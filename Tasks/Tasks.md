# [BRANCHING DIALOGUE SYSTEM]

[FGCT6023: Advanced Games Programming]

[Madeleine Thomas]

[2204696]

### Task 4 Branching Dialogue System

## Research

* I looked up some general websites for dialguw systems for C# to give me a better understanding of the language as I don't use C# often.

* I would avoid using forums as they are usually contradictory and unriliable.

## Development Process

I was placed in a group with George Scanlan and Cayleen Evans-Holmes and together we discussed how we were going to make different outcomes for the dialgue system with one successful and one failure path.

I did some reasearch on some articles for branching dialgue systems for C# as I am not that familiar with the language. There I learnt more about Dialogue nodes and found a handy code snippet.

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
with this knowlage it became easier to visualise how to implement the dialgue system and we worked together to create it.
  
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

### Bibliography

**Apperson, Lem. ‘Beginning Game Development: Dialogue Systems’. Medium, 7 Aug. 2024, https://medium.com/@lemapp09/beginning-game-development-dialogue-systems-0e32147ede77.**

**Crafting Branching Dialogues in Unity: A Guide to Non-Linear Conversations. https://www.linkedin.com/pulse/crafting-branching-dialogues-unity-guide-non-linear-iman-irajdoost-tdwue. Accessed 6 Dec. 2024.**


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

This task gave me a better understanding of C# and I relise how similar it is to C++ in some aspects, using this knowlage I may get into some C# programming languages such as Unity



