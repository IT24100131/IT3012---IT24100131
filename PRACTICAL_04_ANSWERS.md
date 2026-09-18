# IT3012 Practical 04 - Theory-to-Implementation Answers

## 1. Reachability versus feasibility

Reachability is a physical property of the grid. A neighbor is reachable when
it is inside the grid bounds and is not a wall. A reachable cell is not
necessarily safe to enter.

The A* neighbor loop therefore performs the wall and bounds checks first. It
then clears the knowledge base, loads the facts known for that candidate tile,
and runs forward chaining. If the inferred facts contain `Retreat`, the cell
is marked infeasible and is not added to the open list. The knowledge base
therefore adds a logical safety constraint on top of physical reachability.

## 2. Declarative versus procedural paradigms

The knowledge base separates the domain rules from the movement algorithm.
The movement code only performs a general inference operation; it does not
need a new nested `if` statement for every rule.

With a declarative design, adding another rule only requires adding another
premise/conclusion pair. With a procedural design, adding 50 rules would make
the movement method increasingly long, difficult to test, and difficult to
maintain. The knowledge-base approach keeps the inference mechanism stable
while the domain knowledge grows.

## 3. Modus Ponens and Horn clauses

The rule `TargetVisible AND HasDust -> SafeToEngage` is a Horn clause. The
forward-chaining loop checks whether every premise in a rule is already in the
fact set. When all premises are present, it adds the conclusion to the fact
set. This is Modus Ponens: given the premises and the implication, infer the
conclusion.

The loop repeats until a complete pass adds no new facts. This repetition is
needed because a newly inferred conclusion can satisfy the premises of another
rule, such as `SafeToEngage` satisfying the first premise of the `Retreat`
rule.
