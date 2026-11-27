#include <stdio.h>

#define MAX 5   // Maximum number of products

int main()
{
    // Arrays to store product details
    int ids[MAX];
    char names[MAX][20];
    float prices[MAX];
    int quantities[MAX];

    // Helper variables
    int count = 0;
    int choice;
    int i;
    int id;
    int pos;
    int newqty;
    int duplicate;

    // Start the loop and show the menu
    do
    {
        printf("\n====================================\n");
        printf("       PRODUCT INVENTORY SYSTEM\n");
        printf("====================================\n");

        printf("1. Add Product\n");
        printf("2. Search Product\n");
        printf("3. Display All Products\n");
        printf("4. Update Quantity\n");
        printf("5. Exit\n");

        printf("====================================\n");
        printf("Enter your choice (1-5): ");

        if(scanf("%d", &choice) != 1)
        {
            printf("\nInvalid input! Please enter a number.\n");

            while(getchar() != '\n');

            choice = 0;
            continue;
        }

        switch(choice)
        {
            // CASE 1: ADD PRODUCT
            case 1:

                if(count == MAX)
                {
                    printf("\nInventory is full!\n");
                }
                else
                {
                    printf("Enter Product ID: ");
                    scanf("%d", &id);

                    // Check for duplicate ID
                    duplicate = 0;

                    for(i = 0; i < count; i++)
                    {
                        if(ids[i] == id)
                        {
                            duplicate = 1;
                            break;
                        }
                    }

                    if(duplicate == 1)
                    {
                        printf("\nProduct ID already exists!\n");
                    }
                    else
                    {
                        ids[count] = id;

                        printf("Enter Product Name: ");
                        scanf(" %19[^\n]", names[count]);

                        printf("Enter Product Price: ");
                        scanf("%f", &prices[count]);

                        printf("Enter Product Quantity: ");
                        scanf("%d", &quantities[count]);

                        // Validate price and quantity
                        if(prices[count] < 0 || quantities[count] < 0)
                        {
                            printf("\nPrice and quantity cannot be negative!\n");
                        }
                        else
                        {
                            count++;

                            printf("\nProduct added successfully!\n");
                        }
                    }
                }

                break;

            // CASE 2: SEARCH PRODUCT
            case 2:

                if(count == 0)
                {
                    printf("\nInventory is empty!\n");
                }
                else
                {
                    printf("Enter Product ID to search: ");
                    scanf("%d", &id);

                    // Look for the ID
                    pos = -1;

                    for(i = 0; i < count; i++)
                    {
                        if(ids[i] == id)
                        {
                            pos = i;
                            break;
                        }
                    }

                    if(pos == -1)
                    {
                        printf("\nProduct not found!\n");
                    }
                    else
                    {
                        printf("\nProduct found!\n");
                        printf("==============================\n");

                        printf("ID       : %d\n", ids[pos]);
                        printf("Name     : %s\n", names[pos]);
                        printf("Price    : %.2f\n", prices[pos]);
                        printf("Quantity : %d\n", quantities[pos]);

                        printf("==============================\n");
                    }
                }

                break;

            // CASE 3: DISPLAY ALL PRODUCTS
            case 3:

                if(count == 0)
                {
                    printf("\nInventory is empty!\n");
                }
                else
                {
                    printf("\n%-8s %-20s %-12s %-10s\n",
                           "ID", "Name", "Price", "Quantity");

                    printf("--------------------------------------------------\n");

                    // Print every product
                    for(i = 0; i < count; i++)
                    {
                        printf("%-8d %-20s %-12.2f %-10d\n",
                               ids[i], names[i],
                               prices[i], quantities[i]);
                    }
                }

                break;

            // CASE 4: UPDATE QUANTITY
            case 4:

                if(count == 0)
                {
                    printf("\nInventory is empty!\n");
                }
                else
                {
                    printf("Enter Product ID to update: ");
                    scanf("%d", &id);

                    // Search for the product ID
                    pos = -1;

                    for(i = 0; i < count; i++)
                    {
                        if(ids[i] == id)
                        {
                            pos = i;
                            break;
                        }
                    }

                    if(pos == -1)
                    {
                        printf("\nProduct not found!\n");
                    }
                    else
                    {
                        printf("Current Quantity: %d\n",
                               quantities[pos]);

                        printf("Enter new quantity: ");
                        scanf("%d", &newqty);

                        if(newqty < 0)
                        {
                            printf("\nQuantity cannot be negative!\n");
                        }
                        else
                        {
                            quantities[pos] = newqty;

                            printf("\nQuantity updated successfully!\n");
                        }
                    }
                }

                break;

            // CASE 5: EXIT
            case 5:

                printf("\nExiting Program. Goodbye!\n");
                break;

            // DEFAULT CASE
            default:

                printf("\nInvalid choice! Enter 1 to 5.\n");
        }

    } while(choice != 5);

    return 0;
}
