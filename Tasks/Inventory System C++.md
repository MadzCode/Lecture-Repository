# Inventory system
## Bubble sort
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
'''
> ### output
```
{ 
Sorted by Name (Ascending):
Bow: 120
Helmet: 80
Potion: 50
Shield: 100
Sword: 150 
}

> ### full code
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
> # CHAT GPT help

![](./Resources/372512149-dcd8e2cc-10a8-464a-8fa5-2284be199e12.png)

<img width="578" alt="{7DDD759D-E9E8-4064-BCA9-2A41667429B4}" src="https://github.com/user-attachments/assets/dcd8e2cc-10a8-464a-8fa5-2284be199e12">

> ### Bibliography
- “Bubble Sort in C++.” GeeksforGeeks, 2 Feb. 2014, https://www.geeksforgeeks.org/bubble-sort-in-cpp/.
- ChatGPT. https://chatgpt.com. Accessed 1 Oct. 2024.


