-------------------------------------------------
- Wiki | [Home](../../README.md) | [Documentation](../documentation/documentation.md) | [Tutorials](../tutorials/tutorials.md) | [Qualifiers](../qualifiers/qualifier.md) | [Finals](../finals/finals.md)
-------------------------------------------------

# Wiki | Documentation | Scoring

- Scores will be made up of 1) an automatically calculated component and 2) a score based on judges.
- The automatically calculated component for each Trial is a combination of cost and performance metrics.
- A team's final score will be calculated as the sum of scores for each of the competition Trials.
- See [challenge.gov](https://www.challenge.gov/challenge/ariac/) for details on the judges' scoring (scroll to Judging Criteria).
- **Note** that only automated metrics will be used during the qualification rounds of the competition.

## Stability

As outlined in the [update policy](update_policy.md), changes to the scoring metrics may be made between rounds of the competition at the discretion of the competition controllers.
Qualifying teams will be made aware of the final scoring parameters in advance of the Finals of the competition.

## Cost metrics

The cost metrics are calculated from a team's system setup.
Since the same system setup is used for all trials, this value is constant for a team for all trials.
The value in **bold** is used in the final score calculation.

1. **Team System Cost (TC)**: Cost of a team's system. Sum of:
    * $500 for each logical camera used.
    * $500 for each RGBD camera used.
    * $200 for each depth camera used.
    * $100 for each other sensor used.
2. **Baseline System Cost (BC)**: a constant cost amount
3. **Cost Factor (CF)**: A comparison of a team's system cost to the baseline
    * Teams that have the same system cost will have a Cost Factor of 1.
    * Teams with a higher System Cost are penalized by having a Cost Factor < 1
    * `CF = (BC / TC)` where `BC = 1700`

## Performance metrics

Performance metrics cover both completion and efficiency.
They are calculated for each Trial separately.
Completion captures the quality of the shipments submitted; efficiency captures the responsiveness in fulfilling orders.

There are up to two Orders requested during each Trial, each composed of up to two Shipments.
The following values are calculated for each Order requested in a Trial.
The values in **bold** will be used in the final score calculation for a Trial.

## Trial score calculation

1. Shipment Completion Score:
    * sum of:
        * Product presence: 1 point for each correct product touching the tray*
        * All products bonus: points totaling the number of products if all products are present and no unwanted or faulty products are present
        * Product pose: 1 point for each product in the correct pose on the tray. The location must be within 3cm of the target and the orientation must be within 0.1 radians.
    * If the shipment is delivered to the wrong AGV then the shipment score is 0.
2. **Order Completion Score (CS)**:
    * Sum of the Shipment Completion Score for each shipment in the order
3. Order Time (OT):
    * The time taken to complete the order, measured from when the order was first requested
4. Average Time(AT): Average time for all teams to complete the order.
5. **Efficiency Factor (EF)**:
    * A comparison of a team's order time compared to all other teams
    * `EF = AT / OT`
6. **Arm/Arm Collision (AAC)**:
    * 0 if the arms collide with each other, else 1

**note that products must be placed onto the base of the shipping box to count for scoring, not on top of other products.*

## Trial score calculation

The final score for a trial is calculated as follows:

Let `CS{j}`, `EF{j}` be the values for the `j`th order in a trial, `j = 1, 2`

Let `h = 3` as a high-priority factor that encourages quick response to the second (higher priority) order that is issued.

```
Trial Score = AAC * (
                      CF * AVG(CS)
                    + EF1 * CS1
                    + EF2 * CS2 * h
              )
```

-------------------------------------------------
- Wiki | [Home](../../README.md) | [Documentation](../documentation/documentation.md) | [Tutorials](../tutorials/tutorials.md) | [Qualifiers](../qualifiers/qualifier.md) | [Finals](../finals/finals.md)

-------------------------------------------------
