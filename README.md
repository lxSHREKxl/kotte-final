# Bomberman World — Combo Bomber

**Student:** Piotr Jones

## How to play

- **Controls:**
Move with (A, W, S, D), Place bombs with (SPACE), Start/Restart game with (SPACE), Quit the game with (Q)

- **Objective and rules:** 
You win by reaching 500 score, You gain score by exploding enemies. If you explode multiple enemies within a short time, you will gain a combo multiplier which will multiply your earned score.

You lose if you touch an enemy or explode yourself.

Winning takes priority if both conditions are met at the same time.

- **Configurations / demo setup:** default

## Features and validation

| Feature | Check, observed result, and expected behaviour |
| --- | --- |

| 1. Player damage and death | |
I tested the player colliding with all different entities enemies/creates/bombs/powerups/explosions.
The player "died" only when colliding with an enemy or explosion tiles, in my implementation, I change the game state to "Lost" and show a loss screen. Colliding with all other entities remained unchanged and left the player alive. This is the expected outcome.

| 2. Round states and objective | |
I tested entering and exiting every state I added, that included earning enough score to enter the "Win" state and using the Player "death" to enter the "Lose" state. From those states I tested pressing SPACE to restart the game and go back into the "Playing" state.
There were some initial issues for example, the player was able to transition from the "Lose" state to the "Win" state which was not intended, but a simple check for that scenario solved the problem.
In the end, all transitions worked as intended, each state had defined ways to show up on screen and they did, as well as exited to the correct state when intended.

| 3. Safe restart | |
I tested restarting after every ending state, and restarting while bombs and explosions were present in play.
I was getting some initial errors when restarting, that was due to old handles still being used, for example, in the spatial grid, so clearing that vector was the solution.
After that, restarting the map fully refreshes with a new layout of enemies, crates and powerups.
No old information was saved, and the restarted game worked as intended.

| 4. Solid bombs with owner escape | |
I tested placing a bomb and moving in all directions while still inside it, I also tested exiting the bomb and then trying to collide with it. I also tested pressing SPACE multiple times to try to place multiple bombs in one space and then moving while pressing space to see if I used all my bombs in that single space or where they registered as invalid and let me place them elsewhere. I also tested if this mechanic was only present with the player, and enemies would always collide with a bomb.
I was able to move freely while within the newly placed bomb, but once I left it, collision worked correctly, and I couldn't re-enter the bomb. I was also able to place more bombs even after pressing SPACE multiple times at a single space, which is the intended behaviour of not being able to place more than 1 bomb in a single space. Enemies collided with the bomb whilst the player could be inside of it and move freely.

| 5. Blast-range pickup | |
I tested picking up a power-up and placing 2 bombs, expecting only the first to have the bonus blast range. I tested placing a bomb and picking up a power-up before detonation to see if the power-up affected active bombs. I tested the enemies ignoring the power-ups if they walked through them.
Only the first bomb placed after picking up a power-up had the bonus blast range effect, which is the intended behaviour. Enemies walk through power-ups without removing them, while the player can pick up as many as he wants but only saves the effect for the first placed bomb.

| [6. Multiple bombs per owner] | |
I tested placing as many bombs as possible and trying to place more once older bombs exploded.
No new bombs were placed once there were 3 on the map, which was the intended max. Once old bombs exploded, I was able to place more bombs up to 3. This was the intended behaviour.

| [7. Chain reactions] | |
I tested placing 2 bombs within blast range of each other, placing the second one after 1 second to see if the second bomb would detonate together with the first faster than its original fuse timer would allow it to. I also tested this with 3 bombs, expecting the same outcome.
All bombs exploded together as the first bomb exploded, creating a big explosion pattern that all disappeared together. This was the expected behaviour.

| [11. Scoring and combos] | |
I tested exploding an enemy to get the regular score and start the combo timer, and add a score multiplier. I tested exploding multiple enemies within the combo timer to increase it and earn a multiplied score with the increasing score multiplier. I tested waiting for the combo timer to end and seeing the score multiplier drop down and then try to explode another enemy to see if the timer and multiplier start again from the beginning.
The timer started and was dropping correctly whilst increasing on every enemy explosion. The score multiplier was also increasing with every enemy explosion and earning extra score with every exploded enemy until the timer dropped to 0, then the next exploded enemy gave the regular score and started the timer and score multiplier again. This was the intended behaviour.

**Known issues:** None known after testing

## Sources and assistance

This project builds on the shared Kotte foundations.

None beyond the course material


<!-- Submission: commit and push this README with your source to GitHub or the internal Gitea server. Submit the final commit link and a runnable Release ZIP from that version in Studium. Ensure the teacher can access the repository throughout assessment. -->
