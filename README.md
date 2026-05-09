import random

# Global Constants - Mining Configuration
MAX_LAYERS = 3
MAX_ENERGY_SPENT = 100
MIN_ENERGY_SPENT = 1

ROWS = 3
COLS = 3

# Resource Frequency (A is rarest, D is common)
resource_count = {
    "A": 2, # Diamond
    "B": 4, # Gold
    "C": 6, # Silver
    "D": 8, # Stone
}

# Resource Value Multipliers
resource_value = {
    "A": 5,
    "B": 4,
    "C": 3,
    "D": 2,
}

def check_yield(columns, layers, energy, values):
    """Checks the grid for matching resources in horizontal layers."""
    total_yield = 0
    successful_layers = []
    for layer in range(layers):
        resource = columns[0][layer]
        for column in columns:
            resource_to_check = column[layer]
            if resource != resource_to_check:
                break
        else:
            total_yield += values[resource] * energy
            successful_layers.append(layer + 1)
            
    return total_yield, successful_layers

def generate_grid(rows, cols, resources):
    """Generates a random resource grid based on frequency."""
    all_resources = []
    for resource, count in resources.items():
        for _ in range(count):
            all_resources.append(resource)

    columns = []
    for _ in range(cols):
        column = []
        current_resources = all_resources[:]
        for _ in range(rows):
            value = random.choice(current_resources)
            current_resources.remove(value)
            column.append(value)
        columns.append(column)
    
    return columns

def print_grid(columns):
    """Displays the mining grid in a readable format."""
    for row in range(len(columns[0])):
        for i, column in enumerate(columns):
            if i != len(columns) - 1:
                print(column[row], end=" | ")
            else:
                print(column[row], end="")
        print()

def add_energy():
    """Simulates depositing or charging energy units."""
    while True:
        amount = input("How much energy would you like to add? ")
        if amount.isdigit():
            amount = int(amount)
            if amount > 0:
                break
            else:
                print("Amount must be greater than 0.")
        else:
            print("Please enter a valid number.")
    return amount 

def get_number_of_layers():
    """User selects how many layers deep to scan."""
    while True:
        layers = input(f"Enter the number of layers to scan (1-{MAX_LAYERS}): ")
        if layers.isdigit():
            layers = int(layers)
            if 1 <= layers <= MAX_LAYERS:
                break
            else:
                print("Enter a valid number of layers.")
        else:
            print("Please enter a number.")
    return layers

def get_energy_per_layer():
    """User decides how much energy to spend per layer."""
    while True:
        amount = input("Energy to spend per layer? ")
        if amount.isdigit():
            amount = int(amount)
            if MIN_ENERGY_SPENT <= amount <= MAX_ENERGY_SPENT:
                break
            else:
                print(f"Amount must be between {MIN_ENERGY_SPENT} - {MAX_ENERGY_SPENT}.")
        else:
            print("Please enter a number.")
    return amount 

def run_extraction(balance):
    """Handles a single extraction cycle."""
    layers = get_number_of_layers()
    while True:
        energy_spent = get_energy_per_layer()
        total_cost = energy_spent * layers

        if total_cost > balance:
            print(f"Insufficient energy. Your current balance is: {balance} units.")
        else:
            break

    print(f"Scanning {layers} layers. Total energy cost: {total_cost}")
    
    grid = generate_grid(ROWS, COLS, resource_count)
    print_grid(grid)
    
    extraction_yield, successful_layers = check_yield(grid, layers, energy_spent, resource_value)
    
    print(f"Extraction yielded: {extraction_yield} resource units.")
    if successful_layers:
        print(f"Success found on layers:", *successful_layers)
    
    return extraction_yield - total_cost

def main():
    balance = add_energy()
    while True:
        print(f"Current Energy Balance: {balance}")
        answer = input("Press Enter to begin extraction (q to quit).")
        if answer.lower() == "q":
            break
        balance += run_extraction(balance)
        
        if balance <= 0:
            print("You have run out of energy!")
            break

    print(f"Operation ended. Final energy units: {balance}")

if __name__ == "__main__":
    main()
