# python-programing
#task
import random

# Predefined list of 5 words
word_list = ['apple', 'table', 'house', 'smart', 'lucky']

# Randomly choose a word from the list
secret_word = random.choice(word_list)

# Game variables
guessed_letters = []
incorrect_guesses = 0
max_guesses = 6

# Create a display version of the word with underscores
display_word = ['_' for _ in secret_word]

print("🎮 Welcome to Hangman!")
print("Guess the word. You have 6 incorrect guesses allowed.")

# Game loop
while incorrect_guesses < max_guesses and '_' in display_word:
    print("\nCurrent word: ", ' '.join(display_word))
    print("Guessed letters:", ' '.join(guessed_letters))
    
    guess = input("Enter a letter: ").lower()

    # Validate input
    if len(guess) != 1 or not guess.isalpha():
        print("❌ Please enter a single alphabetical character.")
        continue

    if guess in guessed_letters:
        print("⚠ You already guessed that letter.")
        continue

    guessed_letters.append(guess)

    if guess in secret_word:
        print("✅ Good guess!")
        # Update display word
        for i in range(len(secret_word)):
            if secret_word[i] == guess:
                display_word[i] = guess
    else:
        incorrect_guesses += 1
        print(f"❌ Incorrect guess! You have {max_guesses - incorrect_guesses} guesses left.")

# Final result
if '_' not in display_word:
    print("\n🎉 Congratulations! You guessed the word:", secret_word)
else:
    print("\n💀 Game Over! The correct word was:", secret_word)1













    
    #task2
# Hardcoded stock prices
stock_prices = {
    "AAPL": 180,
    "TSLA": 250,
    "GOOGL": 2700,
    "AMZN": 3500,
    "MSFT": 300
}

# Dictionary to store user's portfolio
portfolio = {}

print("📊 Welcome to Stock Portfolio Tracker")
print("Available stocks:", ', '.join(stock_prices.keys()))

# Get user input
while True:
    stock = input("\nEnter stock symbol (or type 'done' to finish): ").upper()
    if stock == 'DONE':
        break
    if stock not in stock_prices:
        print("❌ Stock not in the list. Please choose from:", ', '.join(stock_prices.keys()))
        continue

    try:
        quantity = int(input(f"Enter quantity of {stock} shares: "))
        if quantity < 0:
            print("❌ Quantity can't be negative.")
            continue
        portfolio[stock] = portfolio.get(stock, 0) + quantity
    except ValueError:
        print("❌ Please enter a valid number.")

# Calculate total investment
total_investment = 0
print("\n📈 Your Stock Portfolio:")
for stock, qty in portfolio.items():
    value = qty * stock_prices[stock]
    total_investment += value
    print(f"{stock}: {qty} shares × ${stock_prices[stock]} = ${value}")

print(f"\n💰 Total Investment Value: ${total_investment}")

# Optional: Save to a text file
save = input("\nDo you want to save this portfolio to a file? (yes/no): ").lower()
if save == "yes":
    with open("portfolio.txt", "w") as file:
        file.write("Stock Portfolio Summary\n")
        for stock, qty in portfolio.items():
            value = qty * stock_prices[stock]
            file.write(f"{stock}: {qty} shares × ${stock_prices[stock]} = ${value}\n")
        file.write(f"\nTotal Investment Value: ${total_investment}\n")
    print("📁 Portfolio saved to 'portfolio.txt'")
