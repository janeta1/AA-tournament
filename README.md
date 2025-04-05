# Goal of the strategy

This strategy tries to punish consistent deflection but also rewards cooperation
and offers a second chance to the opponent if they change their behavior.

# Step-by-step breakdown
1. Opening move:
   * The Resettable starts by cooperating. For the next 4 rounds, the Resettable follows a classic
   Tit-for-Tat strategy, i.e. it copies the opponent's last move.
2. Endgame behavior:
   * If we are within 2 rounds of the end (in case the rounds are known),
   the strategy always deflects to avoid being tricked.
3. Mid-game:
   * For every round, the strategy checks the opponent's last
   5 moves:
     * It then calculates the number of times the opponent has cooperated vs deflected.
     * If they deflect more than cooperate -> The strategy considers them untrustworthy and starts a round of deflections.
4. Reset mechanism:
   * The strategy offers forgiveness if all the following conditions are met:
     * The opponent hasn't just started deflecting
     * There has been at least 20 rounds since the last fresh start
     * There are still more than 10 rounds remaining (if the number of rounds is known).
   If these conditions are met, the Resettable cooperates again, offering the opponent
   a chance to establish mutual cooperation.
5. Default behaviour:
    * If none of the conditions above apply, the Resettable defaults to Tit-fot-Tat, making sure
   it's still gaining something