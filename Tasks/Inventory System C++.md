### Inventory system
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

> output

{ 
Sorted by Name (Ascending):
Bow: 120
Helmet: 80
Potion: 50
Shield: 100
Sword: 150 
}