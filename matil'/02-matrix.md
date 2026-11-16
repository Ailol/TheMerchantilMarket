# The g'k matrix

## State, encoding, and mask

Let the logical state set be $S = \{\text{chill}, \text{heat}, \text{center}\}$. Define an injective encoding $e: S \to \mathbb{F}_2^2$ with chill `00`, heat `11`, and center `01`. Addition in this vector space is componentwise modulo two, written XOR. The encoding and the state policy are choices. Once those codes are chosen, the mask for each approved source and destination is determined.

```text
M[a,b] = e(a) ^ e(b)
e(a) ^ M[a,b] = e(b)
```

| From / to | `.` · `00` | `'` · `11` | `·` · `01` |
| --- | --- | --- | --- |
| `.` · `00` | `00` | `11` | `01` |
| `'` · `11` | `11` | `00` | `10` |
| `·` · `01` | `01` | `10` | `00` |

The proof is cancellation: `e(a) ^ e(a) = 00` and `00 ^ e(b) = e(b)`. Uniqueness follows by XORing any proposed solution to `e(a) ^ m = e(b)` with `e(a)`. The table is symmetric, its diagonal is zero, and distinct endpoints have nonzero masks.

This table holds labels for directed edges. It is neither a stochastic transition matrix nor a learned weight matrix. A rule or person chooses the destination. The mask executes the chosen move.

## Composition

For an aligned path `a → b → c`, the intermediate state cancels.

```text
M[a,b] ^ M[b,c]
= e(a) ^ e(b) ^ e(b) ^ e(c)
= M[a,c]
```

| Step | Operation | State |
| --- | --- | --- |
| Start | Read `.` | `00` |
| Heat | Apply `11` | `11` |
| Center | Apply `10` | `01` |
| Net | `11 ^ 10 = 01` | `00 ^ 01 = 01` |

Every closed path reduces to zero. That net value loses the route. A direct `.` → `·` and a path through heat have the same final mask. A diagnostic record can preserve the intermediate state when it matters. Mask XOR is commutative, while the sequence of legal edges still depends on the source of each edge.

## The spare code and the triangle

`10` is a legal **mask** and an unused **state code**. From `11` it reaches `01`, and from `01` it reaches `11`. Applied to `00` it produces the unused state. The fields that contain state codes and masks therefore have distinct meanings even though both fields are two bits wide.

A fixed nonzero XOR on all two-bit words is an involution that partitions the four words into two pairs. No fixed nonzero XOR preserves exactly three states. A three-state cycle needs a source-dependent mask, an explicit next-state table, or a modulo-three operation over a different representation.

The three marks also cannot all be one-bit neighbors. A one-bit move changes the parity of the number of set bits. After three one-bit moves the parity would be different from the start, so such a path cannot be a triangle. This encoding places center one bit away from both other marks and chill two bits away from heat. Each move can still be evaluated by one XOR once its mask is available. [Bennett](06-references.md#computation-and-representation) gives broader context on logical reversibility.

## Applying a move

```text
transition(current, expected_source, target)
    require current and target in {00, 11, 01}
    require current == expected_source
    mask = expected_source XOR target
    result = current XOR mask
    return result
```

This is a specification. A production implementation can use an enum, a table indexed by semantic state IDs, or the encoded values directly. It should reject the unused state code at the boundary. The arithmetic is constant work for these fixed-width values. Selecting a destination, retrieving context, formatting a reply, and displaying it have their own costs. Direct assignment to a known target also takes constant work. A latency comparison needs a real workload and measurements.

A retry of raw `^= mask` can undo a completed move. A retryable request should carry a source version and a target, and then commit only if the version is current. A same-source replay after an intervening round trip is possible when checking the state alone. Versioning identifies that case. If audit history is kept, record the logical target and committed version together rather than treating repeated delivery as a second user move.

## Closing a matrix pass

A closure at the matrix level can retain the selected row, column, mask, and result. A closure at the sum level can retain the net mask for a path. The latter is a sum over $\mathbb{F}_2$, with the operator `^`. A weighted evidence score is a different optional reduction with its own arithmetic and units. The conversation left the choice of reduction open, so the current spec treats the XOR path sum as one reproducible instance of `think'g`.
