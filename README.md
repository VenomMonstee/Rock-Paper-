
# Rock-Paper-

import random

def player(prev_play, opponent_history=[]):
    # Initialize strategy dictionary if it doesn't exist
    if 'strategy' not in player.__dict__:
        player.strategy = {
            'R': 0,
            'P': 0,
            'S': 0
        }
    
    # Function to determine the best counter move
    def counter_move(move):
        if move == 'R':
            return 'P'
        elif move == 'P':
            return 'S'
        else:
            return 'R'

    # Update opponent history
    if prev_play:
        opponent_history.append(prev_play)

    # Update strategy based on opponent history
    if opponent_history:
        last_opponent_move = opponent_history[-1]
        player.strategy[last_opponent_move] += 1

    # Select the move that beats the most frequent move of the opponent
    if opponent_history:
        most_frequent_move = max(player.strategy, key=player.strategy.get)
        next_move = counter_move(most_frequent_move)
    else:
        # If no opponent history, play randomly
        next_move = random.choice(['R', 'P', 'S'])

    return next_move
