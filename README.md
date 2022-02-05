//Contact manage system

#include <stdio.h>
#include <stdlib.h>
#include <string.h>


struct struct_birthday
{
	char day[10];
	char month[10];
	char year[10];
};

typedef struct struct_birthday BIRTHDAY;

struct contact
{
	char first_name[25];
	char last_name[25];
	char company[50];
	char phone_number[25];
	char email[50];
	char working_address[50];
	char home_address[50];
	BIRTHDAY birthday;
};


typedef struct contact CT;


void show(CT list[], int n);
void print_menu();
int location(CT list[], int n);
void add_contact_information(CT &x);
void add_phone_number(CT &x);
void add_birthday(CT &x);
void add_contact(CT list[], int &n);
void edit_contact();
void delete_contact(CT list[], int &n);  // (by name or phone number)
void search_contact(CT list[], int n);  // (by name or phone number)
void list_all_contacts_with_birthdays_in_a_given_month(); //(sort by date)
void list_all_contacts_in_the_table_format(); // (sort by name)

int main()
{	
	CT list[100];
	int n = -1;     // n is top index of list
	char choice;

	do
	{
		system("cls"); 
		print_menu();
		scanf("%c%*c", &choice);

	
		system("cls"); 

		printf("CONTACT KEEPER\n");
		printf("==============\n\n");
	

		switch(choice)
		{
			case '1':	
				add_contact(list, n);
				break;
			case '2':
				edit_contact();
				break;
			case '3':
				delete_contact(list, n);
				break;
			case '4':
				search_contact(list, n);
				break;
			case '5' :
				list_all_contacts_with_birthdays_in_a_given_month();
				break;
			case '6' :
				list_all_contacts_in_the_table_format();
				break;
			case '7' :
				show(list, n);
				break;
		}
		
		if (choice != 'q')
		{	
			printf("\n\n---\n");
			printf("Press any key to back to main menu.");
			getchar();
			fflush(stdin);
		}
	}
	while (choice != 'q');

	return 0;
}


void print_menu()
{
	printf("CONTACT KEEPER\n");
	printf("==============\n\n");
	printf("1. Add Contact\n");
	printf("2. Edit Contact\n");
	printf("3. Delete Contact\n");
	printf("4. Search_contact\n");
	printf("5. List all contacts with birthdays in_a given month\n");
	printf("6. List all contacts in the table format\n");
	printf("7. display list\n");
	printf("q. Quit\n\n");
	printf("Enter your choice (1/2/3/4/5/6/7/q): ");
}


int location(CT list[], int n)
{	
	char choice;
	int i;
	CT temp, x;
	printf("1. Perform operation with name\n");
	printf("2. Perform operation with phone number\n\n");
	printf("Enter your choice (1/2): ");
	scanf("%c", &choice);
	fflush(stdin);
	
	if(choice == '1')
	{
		printf("Enter first name: "); fgets(temp.first_name, sizeof(temp.first_name), stdin);
		printf("Enter last name: "); fgets(temp.last_name, sizeof(temp.last_name), stdin);
		for(i = 0; i <= n; i++)
		{	
			x = list[i]; 
				
			if(strcmp(temp.first_name, x.first_name) == 0 && strcmp(temp.last_name, x.last_name)== 0)
			{	
				return i;
			}
		}
		return -1;
	}
	
	else if(choice == '2')
	{
		add_phone_number(x);
		for(i = 0; i <= n; i++)
		{	
			temp = list[i];
			if(strcmp(temp.phone_number, x.phone_number) == 0)
			{
				return i;
			}
		}
		return -1;
	}
		
	else
		return -2;
	
}


void add_phone_number(CT &x)
{
	int len;
	
	printf("Enter phone number( Phone Number should be a number of 9 or 10 digits): ");
	do
	{
		fgets(x.phone_number, sizeof(x.phone_number), stdin);
		len = strlen(x.phone_number) - 1;

		if(len < 9 || len > 10)
		{	
       		printf("ERROR, Phone Number should be a number of 9 or 10 digits\n");
 			printf("Re-enter phone number: ");
		}
	}
	while(len < 9 || len > 10);
}



void add_birthday(CT &x)
{
	BIRTHDAY B;
	int len1, len2, len3;
	printf("Birthday(DD/MM/YYYY):\n");
	do
	{	
		printf("Enter day: "); scanf("%s", B.day); fflush(stdin);
		printf("Enter month: "); scanf("%s", B.month); fflush(stdin);
		printf("Enter year: "); scanf("%s", B.year); fflush(stdin);
		x.birthday = B;
		len1 = strlen(B.day) ;
		len2 = strlen(B.month) ;
		len3 = strlen(B.year) ;	
		if(len1 != 2 || len2 != 2 || len3 != 4 )
		{
			printf("ERROR, Bithday should be in the DD/MM/YYYY format \n");
			printf("Re-Enter\n");
		}
	}
	while(len1 != 2 || len2 != 2 || len3 != 4);
}


void add_contact_information(CT &x)
{
	printf("Enter first name: "); fgets(x.first_name, sizeof(x.first_name), stdin);
	printf("Enter last name: "); fgets(x.last_name, sizeof(x.last_name), stdin);
	printf("Enter company: "); fgets(x.company, sizeof(x.company), stdin);
	add_phone_number(x);
	printf("Enter email: "); fgets(x.email, sizeof(x.email), stdin);
	printf("Enter working address: "); fgets(x.working_address, sizeof(x.working_address), stdin);
	printf("Enter home address: "); fgets(x.home_address, sizeof(x.home_address), stdin);
	add_birthday(x);
}


void add_contact(CT list[], int &n)
{
	CT x;
	n++;
	
	add_contact_information(x);
	list[n] = x;
	printf("You added successfully");
}


void edit_contact()
{
	printf("Write your code to edit contact here.");
}


void delete_contact(CT list[], int &n)
{	char phone_number_delete[25];
	int i, loc;   // loc = location
	
	printf("Choose 1/2 to delete\n");
	
	loc = location(list, n);
	
	if(loc == -1)
		printf("Not contact found");
	else if	(loc == -2)
		printf("");		
	else
	{	
		for(i = loc; i <= n; i++)
			{	
				list[i] = list[i+1];
			}
		n--;
		printf("You deleted successfully");		
	}
}


void search_contact(CT list[], int n)
{
	int loc = location(list, n);
	CT x = list[loc];
	BIRTHDAY B = x.birthday;
	
	if(loc == -1)
		printf("Not contact found");
	else if(loc == -2)
		printf("");
	else
	{
	printf("First name: %s", x.first_name); 
	printf("Last name: %s", x.last_name); 
	printf("Company: ", x.company);
	printf("Phone number: %s", x.phone_number);
	printf("Email: %s", x.email);
	printf("Working address: %s", x.working_address); 
	printf("Home address: %s", x.home_address);
	printf("Birthday: %s/%s/%s\n", B.day, B.month, B.year);
	}
}


void list_all_contacts_with_birthdays_in_a_given_month()
{
	printf("1");
}


void list_all_contacts_in_the_table_format()
{
	printf("2");
}

void show(CT list[], int n)
{	
	CT x;
	
	
	for(int i = 0; i <= n; i++)
	{	x = list[i];
		BIRTHDAY t = x.birthday;
		printf("           Information of contact %d\n\n", i);
		printf("First name: %s", x.first_name); 
		printf("Last name: %s", x.last_name); 
		printf("Company: ", x.company);
		printf("Phone number: %s", x.phone_number);
		printf("Email: %s", x.email);
		printf("Working address: %s", x.working_address); 
		printf("Home address: %s", x.home_address);
		printf("Birthday: %s/%s/%s\n\n\n", t.day, t.month, t.year);
	}
} 
