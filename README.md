# Iterated Prisoner's Dilemma Evolution Simulator

A browser-based simulation that explores how cooperative strategies evolve through natural selection in the context of the iterated prisoner's dilemma.

## 🎮 Live Demo

**[Launch Simulator →](https://rawcdn.githack.com/emintham/ipd/master/index.html)**

*No installation required - runs entirely in your browser!*

Alternative links:
- [Development Preview](https://raw.githack.com/emintham/ipd/master/index.html) (always latest)
- [HTMLPreview Mirror](https://htmlpreview.github.io/?https://github.com/emintham/ipd/blob/master/index.html)

## Overview

This simulation models a population of individuals with different strategies competing for survival through repeated prisoner's dilemma games. Over time, successful strategies reproduce while unsuccessful ones are eliminated, allowing you to observe evolutionary dynamics in real-time.

## Features

### Three Core Strategies

- **Givers (Green)** - Always cooperate
- **Matchers (Yellow)** - Tit-for-tat: cooperate on first meeting, then mirror opponent's last move
- **Takers (Red)** - Always defect

### Evolution Mechanics

- **Cloning-based reproduction** - Successful individuals are randomly selected to clone
- **Memory inheritance** - Offspring inherit their parent's last 10 interaction memories and grudges
- **Natural selection** - Bottom performers are culled each generation

### Memory & Matching

- **None** - Random matching with no memory influence
- **Affinity** - Individuals prefer to match with cooperators and avoid those who wronged them
  - Requires mutual consent (both must accept the match)
  - 80% preference for non-betrayers, 20% exploration
  - Rejection penalty after 3 consecutive rejections

### Configurable Parameters

#### Population
- Initial counts for each strategy (0-200)

#### Evolution
- **M**: Number of matches before evolution event (10-1000)
- **K**: Number of individuals culled and spawned each generation (1-100)

#### Payoff Matrix
Configure the game-theoretic payoffs:
- **Both Cooperate** - Reward for mutual cooperation (default: 3)
- **Cooperate vs Defect** - Sucker's payoff (default: 0)
- **Defect vs Cooperate** - Temptation to defect (default: 5)
- **Both Defect** - Punishment (default: 1)
- **Rejection Penalty** - Cost of 3 consecutive match rejections (default: -2)

#### Animation
- Speed: 1, 2, 3, 4, 5, 10, 20, or 100 ms per match

## Usage

**Online**: Use the [live demo link](#-live-demo) above

**Local**:
1. Download or clone this repository
2. Open `index.html` in a web browser
3. Configure initial population and parameters using the sliders
4. Click **Play** to start the simulation
5. Use **Pause** to suspend and **Reset** to restart

## How It Works

### Evolution Cycle

1. **Matching** - Individuals are paired for games
   - Random pairing (None mode)
   - Affinity-based with mutual consent (Affinity mode)

2. **Playing** - Each pair plays a prisoner's dilemma game
   - Givers always cooperate
   - Takers always defect
   - Matchers use tit-for-tat strategy

3. **Scoring** - Points awarded based on payoff matrix
   - Scores accumulate over M matches

4. **Evolution** - After M matches:
   - Sort by total score
   - Cull bottom K individuals
   - Randomly clone K survivors
   - Reset scores and reposition

### Memory System

When affinity mode is enabled:

- **Wrongdoing tracked** - If you cooperate and opponent defects, they're marked as a wrongdoer
- **Mutual consent** - Matches only occur if neither party has wronged the other
- **Rejection consequences** - Being rejected 3 times in a row applies a penalty
- **Inheritance** - Offspring inherit parent's last 10 memories and grudges

## Interesting Experiments

1. **Classic Competition**: Start with equal populations and watch which strategy dominates
2. **Taker Invasion**: Start with mostly Givers/Matchers, add a few Takers
3. **Payoff Variations**:
   - Increase cooperation reward to favor Givers
   - Increase temptation to favor Takers
   - Equal all payoffs for neutral selection
4. **Memory Effects**: Compare None vs Affinity modes with different populations
5. **Harsh Environment**: Set rejection penalty to -10 and watch social dynamics

## Game Theory Background

The prisoner's dilemma is a standard game theory scenario where:
- Individual incentive suggests defection
- Collective good requires cooperation
- Iterated play allows reputation and reciprocity to emerge

The classic payoff structure satisfies: **Temptation > Reward > Punishment > Sucker**
(In defaults: 5 > 3 > 1 > 0)

This creates the dilemma: defection dominates in one-shot play, but cooperation can evolve through repeated interactions.

## Technical Details

- Pure client-side JavaScript (no dependencies)
- Canvas-based visualization
- Real-time animation with configurable speed
- Multi-generational memory inheritance

## Statistics Displayed

- **Total Matches** - Cumulative games played
- **Total Individuals** - Current population size
- **Evolution Events** - Number of cull/spawn cycles
- **Generation** - Current generation number
- **Average Scores** - Per-strategy performance metrics
- **Population Distribution** - Visual breakdown by strategy

## License

This is an educational simulation for exploring evolutionary game theory concepts.
