[FGCT6023: Advanced Games Programming]

[Madeleine Thomas]

[2204696]

# Task 1: Inventory Sorting

## Research

* I did some light research into bubble sorting to get a better idea of how it works.

## Development Process

* After some experimentation I realised I was struggling with creating the bubble sort system so I looked to Chat GPT for help and it gave me a code snippet that helped me in fixing the code.

### Chat GPT Code

```cpp
// Function to sort items by name using bubble sort (ascending/descending)
void SortByName(std::vector<Item>& items, bool ascending = true)
{
    int n = items.size();
    for (int i = 0; i < n - 1; ++i)
    {
        for (int j = 0; j < n - i - 1; ++j)
        {
            bool condition = ascending ? (items[j].name > items[j + 1].name) : (items[j].name < items[j + 1].name);
            if (condition)
            {
                std::swap(items[j], items[j + 1]);
            }
        }
    }
}

```

## Working Code

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm> // For std::swap

class Item
{
public:
    std::string name;
    int value;

    Item(std::string n, int v) : name(n), value(v) {}
};

// Function to display the inventory
void DisplayInventory(const std::vector<Item>& items)
{
    for (const auto& item : items)
    {
        std::cout << item.name << ": " << item.value << std::endl;
    }
}

// Function to sort items by name using bubble sort (ascending/descending)
void SortByName(std::vector<Item>& items, bool ascending = true)
{
    int n = items.size();
    for (int i = 0; i < n - 1; ++i)
    {
        for (int j = 0; j < n - i - 1; ++j)
        {
            bool condition = ascending ? (items[j].name > items[j + 1].name) : (items[j].name < items[j + 1].name);
            if (condition)
            {
                std::swap(items[j], items[j + 1]);
            }
        }
    }
}

// Function to sort items by value (ascending/descending)
void SortByValue(std::vector<Item>& items, bool ascending = true)
{
    if (ascending)
        std::sort(items.begin(), items.end(), [](const Item& a, const Item& b) { return a.value < b.value; });
    else
        std::sort(items.begin(), items.end(), [](const Item& a, const Item& b) { return a.value > b.value; });
}

int main()
{
    std::vector<Item> items = {
        Item("Sword", 150),
        Item("Potion", 50),
        Item("Shield", 100),
        Item("Bow", 120),
        Item("Helmet", 80)
    };

    std::cout << "Original Inventory:" << std::endl;
    DisplayInventory(items);

    std::cout << "\nSorted by Name (Ascending):" << std::endl;
    SortByName(items, true); // Sort by name in ascending order
    DisplayInventory(items);

    std::cout << "\nSorted by Value (Descending):" << std::endl;
    SortByValue(items, false); // Sort by value in descending order
    DisplayInventory(items);

    return 0;
}

```

## Reflection

* Even though I struggled to complete this task by myself, I learned more about bubble sort and how to use bubble sort 

## Bibliography

**‘Bubble Sort in C++’. GeeksforGeeks, 2 Feb. 2014, https://www.geeksforgeeks.org/bubble-sort-in-cpp/.**

**ChatGPT. https://chatgpt.com. Accessed 6 Dec. 2024.**

# Task 2: Educational Game Plan

## Research 

* For this Trello board I researched steps on how to achieve good workflow such as setting smart goals for the team and not overloading them, mapping out the workflow design which is what I did with the Trello Board and designating roles in the team so nobody is outside of their comfort zone and is able to work effectivlty. 

## Development Process

* For the first sprint It was for allowing the team to get a feel for one another and start production on their different mechanics.

* The second sprint was for making the game be in a testable state, e.g. creating animations and finalising core gameplay.

* The third sprint was for polishing the game and finalising all of gameplay so it is ready to be published.

## Trello Board

![image](https://github.com/user-attachments/assets/25628bbd-72b6-460f-9683-85398b81ee0f)

## Reflection

* Creating this board allowed me to better visualise how group workflows will work. This will be especially helpful for my final project where I will be working on a group project.

## Bibliography

**Trello. https://trello.com/b/if69IpyM. Accessed 6 Dec. 2024.**

**Gluchovskis, Mindaugas. 11 Steps to Build a Successful Workflow Across Teams - Teamhood. 13 Feb. 2024, https://teamhood.com/team-performance/successful-workflow-across-teams/.**

# Task 3: Health Potion Optimization

## Research

* I did some research on Object Oriented Language and how I could possibly use that knowlage to better understand how I could implement a health potion system.

## Development Process

* I was put into a group with George Scanlan and together we experimented with if statements to try and make the health potion system.

* We made some if else statementes to help make it so the health is filled to the maximum without going over.

* We tried to make it so that it would output the amount of potions but that would just break the project.

### Working Code

```cpp

#include <iostream>
#include <vector>
#include <algorithm>

// Define a Potion class
class Potion {
public:
    std::string name;
    int healingValue;

    Potion(std::string name, int healingValue) : name(name), healingValue(healingValue) {}
};

// Define a Player class
class Player {
public:
    std::string name;
    int currentHealth;
    int maxHealth;

    Player(std::string name, int currentHealth, int maxHealth) : name(name), currentHealth(currentHealth), maxHealth(maxHealth) {}
};

// Define a HealthPotionsSystem class
class HealthPotionsSystem {
public:
    std::vector<Potion> potions;

    HealthPotionsSystem() {
        // Adding multiple potions
        potions.push_back(Potion("Small Potion", 10));
        potions.push_back(Potion("Medium Potion", 20));
        potions.push_back(Potion("Large Potion", 50));
    }

    // Method to determine the optimal potions to consume for each player
    void HealPlayers(std::vector<Player>& players) {
        for (auto& player : players) {
            int healthNeeded = player.maxHealth - player.currentHealth;
            if (healthNeeded == 0) {
                std::cout << player.name << " is already at max health!" << std::endl;
                continue;
            }

            // Sort potions by their healing value in descending order
            std::sort(potions.begin(), potions.end(), [](const Potion& p1, const Potion& p2) {
                return p1.healingValue > p2.healingValue;
            });

            // Heal player with the optimal potions
            while (player.currentHealth < player.maxHealth) {
                if (healthNeeded >= 50) {
                    player.currentHealth += 50;
                } else if (healthNeeded >= 20) {
                    player.currentHealth += 20;
                } else if (healthNeeded >= 10) {
                    player.currentHealth += 10;
                } else {
                    player.currentHealth = player.maxHealth;
                }

                if (player.currentHealth > player.maxHealth) {
                    player.currentHealth = player.maxHealth;
                }

                std::cout << "Healing " << player.name << ": Current Health = " << player.currentHealth << ", Max Health = " << player.maxHealth << std::endl;
                healthNeeded = player.maxHealth - player.currentHealth;
                if (player.currentHealth < player.maxHealth) {
                    std::cout << "Not enough potions to fully heal " << player.name << "!" << std::endl;
                } else {
                    std::cout << player.name << " is fully healed!" << std::endl;
                }
            }
        }
    }
};

int main() {
    // List of multiple players
    std::vector<Player> players = {
        Player("Mage", 50, 100),
        Player("Knight", 70, 100),
        Player("Rogue", 60, 100),
        Player("Cleric", 85, 100)
    };

    HealthPotionsSystem potionsSystem;
    potionsSystem.HealPlayers(players); // Heal all players optimally using available potions

    return 0;
}
```

### Reflection

* Even though we did not manage to get the code to output the amount of potions, we did fix the health bug and it taught me more about bug fixing in C++ as when I usually get an error it is hard for me to find the cause of it. I now know to narrow it down into smaller chunks and work from there.

### Bibliography

**‘Object Oriented Programming in C++’. GeeksforGeeks, 8 Aug. 2015, https://www.geeksforgeeks.org/object-oriented-programming-in-cpp/.**

# Task 4: Branching Dialogue System

## Research

* I looked up some general websites for dialogue systems for C# to give me a better understanding of the language as I don't use C# often.

* I would avoid using forums as they are usually contradictory and unriliable.

## Development Process

* I was placed in a group with George Scanlan and Cayleen Evans-Holmes and together we discussed how we were going to make different outcomes for the dialgue system with one successful and one failure path.

* I did some reasearch on some articles for branching dialgue systems for C# as I am not that familiar with the language. There I learnt more about Dialogue nodes and found a handy code snippet.

```csharp

public class DialogueNode
{
    public string DialogueText { get; set; }
    public List<Choice> Choices { get; set; }

    public DialogueNode(string dialogueText)
    {
        DialogueText = dialogueText;
        Choices = new List<Choice>();
    }
}

public class Choice
{
    public string ChoiceText { get; set; }
    public DialogueNode NextNode { get; set; }

    public Choice(string choiceText, DialogueNode nextNode)
    {
        ChoiceText = choiceText;
        NextNode = nextNode;
    }
}
```
```
```
* with this knowlage it became easier to visualise how to implement the dialgue system and we worked together to create it.
  
### Working Code

```csharp

using System;
using System.Collections.Generic;

// The DialogueNode class represents a single dialogue option in the tree
public class DialogueNode
{
    public string DialogueText { get; set; }      // The dialogue text for the node
    public List<DialogueChoice> Choices { get; set; }  // Choices for the player to make

    // Constructor for initializing dialogue nodes
    public DialogueNode(string dialogueText)
    {
        DialogueText = dialogueText;
        Choices = new List<DialogueChoice>();  // Initialize the list of choices
    }

    // Method to add a choice to this node
    public void AddChoice(string choiceText, DialogueNode nextNode)
    {
        Choices.Add(new DialogueChoice(choiceText, nextNode));
    }
}

// The DialogueChoice class represents a player's choice and the resulting dialogue node
public class DialogueChoice
{
    public string ChoiceText { get; set; }  // Text of the player's choice
    public DialogueNode NextNode { get; set; }  // The next dialogue node based on the player's choice

    // Constructor for initializing a choice
    public DialogueChoice(string choiceText, DialogueNode nextNode)
    {
        ChoiceText = choiceText;
        NextNode = nextNode;
    }
}

// The DialogueSystem class represents the overall dialogue system
public class DialogueSystem
{
    public DialogueNode RootNode { get; private set; }  // The starting point of the conversation
    private DialogueNode CurrentNode;  // Tracks the current node in the conversation

    // Constructor that sets the root node
    public DialogueSystem(DialogueNode rootNode)
    {
        RootNode = rootNode;
        CurrentNode = rootNode;  // Start at the root node
    }

    // Method to build the dialogue tree
    public void BuildDialogueTree()
    {
        // Example of building the dialogue tree:
        DialogueNode introduction = new DialogueNode("Hello! How can I help you today?");
        DialogueNode weather = new DialogueNode("The weather is great! It's sunny outside.");
        DialogueNode directions = new DialogueNode("You need to head north and then turn left.");
        DialogueNode goodfarewell = new DialogueNode("Goodbye! Have a nice day.");
        DialogueNode badfarewell = new DialogueNode("Bye. Have a nice day.");

        // Add choices to the root node
        introduction.AddChoice("Tell me about the weather.", weather);
        introduction.AddChoice("I need directions.", directions);
        introduction.AddChoice("Nothing, just passing by.", badfarewell);

        // Add choices to the weather node
        weather.AddChoice("Thanks!", goodfarewell);

        // Add choices to the directions node
        directions.AddChoice("Thanks for the directions!", goodfarewell);

        // Now, set the root node in the DialogueSystem to the introduction
        RootNode = introduction;
        CurrentNode = RootNode; // Reset the current node to the root after building the tree
    }

    // Method to start the dialogue
    public void StartDialogue()
    {
        while (true)
        {
            // Display the current node's dialogue text
            Console.Clear();
            Console.WriteLine(CurrentNode.DialogueText);

            // If there are no choices, end the conversation
            if (CurrentNode.Choices.Count == 0)
            {
                Console.WriteLine("End of conversation.");
                break;
            }

            // Display the player's choices
            Console.WriteLine("\nChoose an option:");
            for (int i = 0; i < CurrentNode.Choices.Count; i++)
            {
                Console.WriteLine($"{i + 1}. {CurrentNode.Choices[i].ChoiceText}");
            }

            // Get the player's choice
            int choice = 0;
            while (choice < 1 || choice > CurrentNode.Choices.Count)
            {
                Console.Write("Enter the number of your choice: ");
                bool isValidChoice = int.TryParse(Console.ReadLine(), out choice);

                if (!isValidChoice || choice < 1 || choice > CurrentNode.Choices.Count)
                {
                    Console.WriteLine("Invalid choice. Please try again.");
                }
            }

            // Navigate to the next dialogue node based on the player's choice
            CurrentNode = CurrentNode.Choices[choice - 1].NextNode;
        }
    }
}

// The Program class starts the dialogue system
public class Program
{
    public static void Main(string[] args)
    {
        // Build the dialogue tree and start the dialogue
        DialogueSystem dialogueSystem = new DialogueSystem(null);  // Initialize with null, will set RootNode later
        dialogueSystem.BuildDialogueTree();  // Build the dialogue structure
        dialogueSystem.StartDialogue();      // Start navigating through the dialogue
    }
}
```

### Reflection

* This task gave me a better understanding of C# and I relise how similar it is to C++ in some aspects, using this knowlage I may get into some C# programming languages such as Unity

### Bibliography

**Apperson, Lem. ‘Beginning Game Development: Dialogue Systems’. Medium, 7 Aug. 2024, https://medium.com/@lemapp09/beginning-game-development-dialogue-systems-0e32147ede77.**

**Crafting Branching Dialogues in Unity: A Guide to Non-Linear Conversations. https://www.linkedin.com/pulse/crafting-branching-dialogues-unity-guide-non-linear-iman-irajdoost-tdwue. Accessed 6 Dec. 2024.**



