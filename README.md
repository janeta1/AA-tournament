# Goal of the strategy

The **Resettable** strategy is designed to punish consistent defection while rewarding cooperation.
It also includes a reset mechanism that offers opponents a second chance if they demonstrate a willingness to change their behavior.

The main goal is to maximize long-term gains by building trust when possible, but without being naive to repeated betrayal.


# Round 1: Strategy Implementation:
## Step-by-step breakdown
1. **_Opening move:_**
   * The Resettable starts by cooperating. 
   * For the next 4 rounds, the Resettable follows a classic
   Tit-for-Tat strategy, i.e. it copies the opponent's last move. This builds early trust while staying alert to any signs of defection.
2. _**Endgame behavior:**_
   * If we are within 2 rounds of the end (in case the rounds are known),
   the strategy always deflects to avoid being tricked. This ensures that the opponent cannot exploit the final rounds by suddenly defecting after a period of cooperation.

3. **_Mid-game:_**
   * For every round, the strategy checks the opponent's last
   5 moves:
     * It then calculates the number of times the opponent has cooperated vs deflected.
     * If they deflect more than cooperate - The strategy considers them untrustworthy and starts a round of deflections.
   * This dynamic adjustment helps protect against opponents who gradually become less cooperative over time.
4. **_Reset mechanism:_**
   * The Resettable includes a built-in forgiveness mechanism to encourage recovery of cooperation. It resets and offers cooperation again only if all of the following conditions are met:
     * The opponent hasn't just started deflecting
     * There has been at least 20 rounds since the last fresh start
     * There are still more than 10 rounds remaining (if the number of rounds is known).
   * If these conditions are satisfied the Resettable initiates a fresh start, cooperating again to see if the opponent is willing to rebuild trust. This mechanism helps avoid long-term cycles of mutual punishment and gives the opponent a meaningful opportunity to improve.
5. **_Default behaviour:_**
    * If none of the conditions above apply, the Resettable defaults to Tit-fot-Tat, making sure
   it's still gaining something


# Round 2: Opponent Selection

In addition to determining its next move, the Resettable strategy also intelligently chooses which opponent to face next in Round 2.

Here’s how the opponent selection works step-by-step:
1. **_Prioritize unplayed opponents:_**
   * The algorithm first checks if there are any opponents it has played fewer than 10 rounds against.
   * If such opponents exist, the strategy picks the first one to ensure it gathers information about every player early on.
2. **_Score-based evaluation:_**
   * If all opponents have been sufficiently explored, the strategy evaluates opponents based on past performance.
   * It calculates a score for each opponent based on:
     * The cumulative payoff received so far (using standard Prisoner's Dilemma payoffs: (C, C) = 3, (C, D) = 0, (D, C) = 5, (D, D) = 1).
     * The opponent’s cooperation rate — how often they have cooperated across all past rounds.
   * The formula gives an extra weight to cooperation, rewarding opponents who are more likely to cooperate with it.
3. **_Opponent selection:_**
   * After computing these scores, the strategy sorts all opponents based on the combined value (payoff + cooperation bonus).
   * It selects the opponent with the highest score for the next interaction.
4. **_Fallback:_**
   * If no information is available (for instance, if the histories are empty), the strategy defaults to continuing against the current opponent to avoid errors.


# Summary
The Resettable is a flexible and resilient strategy that can handle many types of opponents:

* It builds early cooperation.
* It punishes when necessary.
* It forgives intelligently.
* It defends against late-game betrayals.
* It dynamically selects the next opponent based on past interactions.

Through this careful balance, it aims to achieve high scores while minimizing risks in both short and long-term interactions.


