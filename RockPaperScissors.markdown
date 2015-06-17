#Rock, Paper, Scissors
This game was a variation of the classic childrens game we all love.  The game was made up of two classes and a file app.rb which brought it all together.  The player class, kept track of player information such as score, name and the move played each round.  The game class kept track of number of rounds in a game, acceptable moves, and a hash with key => value pair of winning plays => losing plays.

App.rb played the game as a loop that would continue as long as the players score was lower than half of the games to be played, plus one.  The continue method was in the game class.

```ruby
while newgame.continue?(player1.score, player2.score) == true
```

```ruby
  def continue?(player1_score, player2_score)
    player1_score < to_win && player2_score < to_win
  end
```

All of the puts and gets statements in the program are in app.rb which include getting the player names and plays as well as whether or not to play against AI when dealing with player 2.

```ruby
  if player2.name == "Computer"
    player2.play = newgame.answers.sample
    puts "\n Computer played #{player2.play}"
  else
    puts "\n #{player2.name} the choice is yours... Rock, Paper, or Scissors?"
    player2.play = gets.chomp.downcase
      
    if newgame.acceptable_play?(player1.play) == false
      puts "That is not an acceptable play, try again."
    end
  end
```


And then after the game is over, app.rb puts the winner and the score of the match.

```ruby
case newgame.game_over(player1.score, player2.score)
when true
  puts "\n #{player1.name} wins with a score of #{player1.score} - #{player2.score}."
when false
  puts "\n #{player2.name} wins with a score of #{player2.score} - #{player1.score}."
end
```


##The Game class

The game class determines critical functions of the rock paper scissors game with methods that

-acceptable plays:
```ruby
  def acceptable_play?(play)
    @answers.include? play
  end
```
This method checked the choice played each round against the array of acceptable plays.


-score needed to win:
```ruby
  def to_win
    (@rounds / 2) + 1
  end
```
This method took the number of rounds(preferably an odd number) and divided it by 2.  3/2 returns 1 in ruby since the numbers are stored as an integer.  So (3/2) + 1 made it so in order to win a best of 3, you needed to win 2 games.


-whether or not to continue after each round:
```ruby
  def continue?(player1_score, player2_score)
    player1_score < to_win && player2_score < to_win
  end
```

This method would contine the game as long as player1 and player2 both had scores less than the number of wins needed defined in the method above.


-who won when the game is over:
```ruby
  def game_over(player1_score, player2_score)
    player1_score > player2_score
  end
```
This method determined the winner for each round by comparing players choices to the @winning_combos hash key|value pairs.



##The Player class

The player class was very simple and had no methods other than initializing to store the variables for name, score and play.

```ruby
  def initialize
    @name = name
    @play = play
    @score = 0
  end
```


