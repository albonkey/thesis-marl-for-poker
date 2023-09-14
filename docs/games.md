# Index
*   [Leduc Hold'em](games.md#leduc-holdem)
*   [Limit Texas Hold'em](games.md#limit-texas-holdem)
*   [No-limit Texas Hold'em](games.md#no-limit-texas-holdem)

## Leduc Hold'em
Leduc Hold'em is a smaller version of Limit Texas Hold'em (first
introduced in [Bayes' Bluff: Opponent Modeling in Poker](http://poker.cs.ualberta.ca/publications/UAI05.pdf)). The deck consists only two pairs of King, Queen and Jack, six cards in total. Each game is fixed with two players, two rounds, two-bet maximum and raise amounts of 2 and 4 in the first and second round. In the first round, one player is randomly choosed to put 1 unit in pot as small blind while the other puts 2 unit as big blind, and each player is dealt one card, then starts betting. The player with small blind acts first. In the second round, one public card is revealed first, then the players bet again. Finally, the player whose hand has the same rank as the public card is the winner. If neither, then the one with higher rank wins. Other rules such as 'fold' can refer to Limit Texas hold'em.

### State Representation of Leduc Hold'em
The state is encoded as a vector of length 36. The first 3 elements correspond to hand card. The next 3 elements correspond to public card. The last 30 elements correspond the chips of the current player and the opponent (the chips could be in range 0~14) The correspondence between the index and the card is as below.

| Index   | Meaning                              |
| --------| :-----------------------------------:|
| 0~2     | J ~ K in hand                        |
| 3~5     | J ~ K as public card                 |
| 6~20    | 0 ~ 14 chips for the current player  |
| 21~35   | 0 ~ 14 chips for the opponent        |

### Action Encoding of Leduc Hold'em
The action encoding is the same as Limit Hold'em game.

### Payoff of Leduc Hold'em
The payoff is calculated similarly with Limit Hold'em game.

## Limit Texas Hold'em
Texas Hold'em is a popular betting game. Each player is dealt two face-down cards, called hole cards. Then 5 community cards are dealt in three stages (the flop, the turn and the river). Each player seeks the five best cards among the hole cards and community cards. There are 4 betting rounds. During each round each player can choose "call", "check", "raise", or "fold".

In fixed limit Texas Hold'em. Each player can only choose a fixed amount of raise. And in each round the number of raises is limited to 4.

### State Representation of Limit Texas Hold'em
The state is encoded as a vector of length 72. The first 52 elements represent cards, where each element corresponds to one card. The hand is represented as the two hole cards plus the observed community cards so far. The last 20 elements are the betting history. The correspondence between the index and the card is as below.

| Index   | Meaning                 |
| ------- | :----------------------:|
| 0~12    | Spade A ~ Spade K       |
| 13~25   | Heart A ~ Heart K       |
| 26~38   | Diamond A ~ Diamond K   |
| 39~51   | Club A ~ Club K         |
| 52~56   | Raise number in round 1 |
| 57~61   | Raise number in round 2 |
| 62~66   | Raise number in round 3 |
| 67~71   | Raise number in round 4 |

### Action Encoding of Limit Texas Hold'em
There 4 actions in Limit Texas Hold'em. They are encoded as below.

| Action ID   |     Action    |
| ----------- | :------------ |
| 0           | Call          |
| 1           | Raise         |
| 2           | Fold          |
| 3           | Check         |

### Payoff of Limit Texas Hold'em
The stardard unit used in the literature is milli big blinds per hand (mbb/h). In the toolkit, the reward is calculated based on big blinds per hand. For example, a reward of 0.5 (-0.5) means that the player wins (loses) 0.5 times of the amount of big blind.

## No-limit Texas Hold'em
No-limit Texas Hold'em has similar rule with Limit Texas Hold'em. But unlike in Limit Texas Hold'em game in which each player can only choose a fixed amount of raise and the number of raises is limited. In No-limit Texas Hold'em, the player may raise with at least the same amount as previous raised amount in the same round (or the minimum raise amount set before the game if none has raised), and up to the player's remaining stack. The number of raises is also unlimited.

## State Representation of No-Limit Texas Hold'em
The state representation is similar to Limit Hold'em game. The state is represented as 52 cards and 2 elements of the chips of the players as below:

| Index   | Meaning                            |
| ------- | :--------------------------------- |
| 0~12    | Spade A ~ Spade K                  |
| 13~25   | Heart A ~ Heart K                  |
| 26~38   | Diamond A ~ Diamond K              |
| 39~51   | Club A ~ Club K                    |
| 52      | Chips of player 1                  |
| 53      | Chips that all players have put in |

### Action Encoding of No-Limit Texas Hold'em
There are 103 actions in No-limit Texas Hold'em. They are encoded as below.

<small><sup>*</sup>Note: Starting from Action ID 3, the action means the amount player should put in the pot when chooses 'Raise'. The action ID from 3 to 5 corresponds to the bet amount from half amount of the pot, full amount of the pot to all in.</small>

| Action ID   |     Action         |
| ----------- | :----------------- |
| 0           | Fold               |
| 1           | Check              |
| 2           | Call               |
| 3           | Raise Half Pot     |
| 4           | Raise Full Pot     |
| 5           | All In             |

### Payoff of No-Limit Texas Hold'em
The reward is calculated based on big blinds per hand. For example, a reward of 0.5 (-0.5) means that the player wins (loses) 0.5 times of the amount of big blind.
