/*
Names of Group Members:

Occurence: UN1
Tutorial Teacher: Oniel Charles
Chevannese Ellis 2301109 
Jonathan Blackwood 2306822
Gabby Tucker 2206681

Occurrences: UE2
Tutorial Teacher: Mrs. Aleisa Bowen-Mighty
Shanoi Walker-Gayle 1808177

Description: Stateline Gas Station Programming 2 Major Project

The default password to access admin features is set to bruh
*/
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>
#include <ctype.h>
#define SIZE 100

//Declarations of Enums
enum CustType 
{
	CASH = 1, CHARGE = 2
};

enum FUEL_TYPE
{
	E10_87 = 1, E10_90 = 2, DIESEL = 3
};

enum PREFERENCE 
{
	DEPOSIT = 0, MAXIMUM = 1
};

enum PAYMENT_TYPE
{
    CARDCASH = 1, CHEQUE = 2  
};

enum REPORT_TYPE
{
  SALES_REPORT = 1, CHARGE_REPORT = 2, FUEL_REPORT = 3
};

//Declarations of Structs
typedef struct {
	char cust_type [6];
	char fuel_type[9];
	float fuel_amount;
	float money;
	float change;
	char lubricant[6];
	float lubricant_amount;
	float gct_amount;
	float sub_total;
	float grand_total;
}Customer;

typedef struct {
	int id;
	char name[51];
	char licenses[5][7];
	int representatives;
	char fuel_type[9];
	char preference[9];
	char lubricant[6];
	float lubricant_amount;
	float fuel_amount;
	int preference_number;
	float money;
	float current_money;
	float initial_money;
	float litres;
	float current_litres;
	float initial_litres;
	float gct_amount;
	float sub_total;
	float grand_total;
	float change;
}ChargeCustomer;

//Global Variables that manages the list 
int chargelist = 3, serve_list = 0, overall_list = 0;
int current_charge_id = 4;
int chargecount;
//Global Variables of Serve Customer 
int cust_type, option, cod_type, fuel, lub, cashcount = 0, charge_count = 0;
float money;
const char fuel_types[][7] = {"None","E10-87","E10-90","Diesel"};
const char lubricant_types[][7] = {"None","5W-30","5W-40","15W-40","SAE-40"};
const char preference_method[][8] = {"DEPOSIT","MAXIMUM"};
const float lub_price[6] = {0, 2900, 3500, 3600, 2100};
const float fuel_per_litre[5] = {0, 184.90, 193.60, 182.30};
const float  min_money_card = 1000.00, min_litre_cash = 2.00;
//Global Variables of Add Charge Customer
char license [7];
int reps, id, item_count, current_customer;
const float min_deposit = 10000, max_litres = 3785.41, min_cheque = 5000;
//Global Variables of Make Payment to Charge Customer
int type_pay;
float payment;
float payment_litre;
//Global Variables that Update Charge Customer
int field_option, field_type;
//Global Variables that Refuel Tank
const float FUEL_TANK_CAPACITY[5] = {0, 75708.23, 113562.35, 94635.29};
const float refuel_per_gallon [5] = {0, 165.64, 171.74, 159.38};
float CURRENT_FUEL_TANK_CAPACITY [5] = {0, 75708.23, 113562.35, 94635.29};
float refuel_amount;
//Global Variables of Generate Report
int report_option;
float FUEL_SALES[5] = {0, 0, 0, 0};
float TOTAL_LITRES = 0;
float SALES_GRAND_TOTAL[4] = {0, 0, 0};

//ProtoType Functions
char luq_req();
char generate_preference();
const char *get_current_date();
float accumulate_fuel_sales();
float accumulate_fuel_sales2();
float accumulate_litres();
float accumulate_litres2();
float convert_gallon_to_litres(float x);
float gallon();
float gct();
float litre();
int login();
int search_id(ChargeCustomer *client, int key);
int search_reps(ChargeCustomer *client, int key);
void add_charge_customer(ChargeCustomer *ptrclient);
void payment_charge_customer(ChargeCustomer *ptrclient);
void deposit_serve(ChargeCustomer *ptrclient);
void create_default_customers(ChargeCustomer *ptrclient);
void prompt_int_range(const char *message, int *option, int min, int max, const char *error);
void generate_license(ChargeCustomer *ptrcust, int i);
void generate_preference_output(ChargeCustomer *ptrclient);
void generate_report(ChargeCustomer *ptrclient);
void receipt1(Customer *ptrcust);
void receipt2(ChargeCustomer *ptrclient);
void refuel_tank();
void refuel_tank_output();
void remove_charge_customer(ChargeCustomer *ptrclient);
void saveToFileCash(FILE *fcashcust, Customer *ptr);
void saveToFileCharge(FILE *fchargecust, ChargeCustomer *ptclient);
void saveToFileCharge2(FILE *fchargecust2, ChargeCustomer *ptclient);
void serve_customer(Customer *ptrcust, ChargeCustomer *ptrclient);
void update_charge_customer(ChargeCustomer *ptrclient);

int main()
{
    FILE *fcashcust;
    FILE *fchargecust;
    FILE *fchargecust2;
    fcashcust = fopen("CashCustomerData.txt","a");
    fchargecust = fopen("ChargeCustomerData.txt", "w");
    fchargecust2 = fopen("List_of_representatives.txt", "w");
    
    srand(time(NULL));
    Customer customer[SIZE];
    Customer *ptrcust = customer;
    ChargeCustomer client[SIZE];
    ChargeCustomer *ptrclient = client;
    create_default_customers(ptrclient);
    while (1) {
		printf("1 - Serve Customer\n" 
				"2 - Add Charge Customer\n" 
				"3 - Update Charge Customer\n" 
				"4 - Delete Charge Customer\n" 
				"5 - Make Payment to Charge Account\n" 
				"6 - Refuel Tank\n" 
				"7 - Generate Report\n" 
				"8 - Exit\n" 
				"Enter a option (1 - 8): ");
		scanf("%d", &option);
		switch (option)
		{
		    case 1:
		        if(overall_list < SIZE)
		        {
		            serve_customer(ptrcust,ptrclient);
		        }
		        else
		        {
		            puts("The system has reached max capacity for the day");
		        }
		        break;
		    case 2:
		        if (overall_list < SIZE)
		        {
		            add_charge_customer(ptrclient);
		        }
		        else
		        {
		            puts("The system has reached max capacity for the day");
		        }
		        break;
		    case 3:
		        update_charge_customer(ptrclient);
		        break;
		    case 4:
		        remove_charge_customer(ptrclient);
		        break;
		    case 5:
		        payment_charge_customer(ptrclient);
		        break;
		    case 6:
		        refuel_tank();
		        break;
		    case 7:
		        generate_report(ptrclient);
		        break;
		    case 8:
		        saveToFileCash(fcashcust,ptrcust);
		        saveToFileCharge(fchargecust,ptrclient);
		        saveToFileCharge2(fchargecust2,ptrclient);
		        return 0;
		        break;
		    default:
		        puts("Invalid Option");
		}
		puts("");
    }
    return 0;
}


char lub_req()
{
    const char lub[2] = {'Y','N'};
    return lub [rand() % 2];
}

char generate_preference()
{
    const char pre[2] = {'D','M'};
    return pre[rand() % 2];
}

//Generates a response based on generate_preference()
void generate_preference_output(ChargeCustomer *ptrclient)
{
  int response = generate_preference();
  printf("Generating Preference: %c\n",response);
  if (response == 'D')
  {
    puts("Preference Deposit has been assigned to customer");
    ptrclient[current_customer].preference_number = DEPOSIT;
    strcpy(ptrclient[current_customer].preference, preference_method[DEPOSIT]);
  }
  else if (response == 'M')
  {
    puts("Preference Maximum litres has been assigned to customer");
    ptrclient[current_customer].preference_number = MAXIMUM;
    strcpy(ptrclient[current_customer].preference,preference_method[DEPOSIT]);
  }
}

//Returns the current date as a string
const char *get_current_date() {
	static char date[11];
	const time_t clock = time(NULL);
	struct tm *time = localtime(&clock);
	strftime(date, 11, "%d/%m/%Y", time);
	return date;
}

//Accumulates each fuel type sales
float accumulate_fuel_sales2()
{
 
  switch(fuel)
  {
    case E10_87:
      return FUEL_SALES[E10_87] +=  payment_litre * fuel_per_litre[fuel];
    case E10_90:
      return FUEL_SALES[E10_90] +=  payment_litre * fuel_per_litre[fuel];
    case DIESEL:
      return FUEL_SALES[DIESEL] +=  payment_litre * fuel_per_litre[fuel];
  }
}

//Accumulates each fuel type sales on maximum litres charge customers
float accumulate_fuel_sales()
{
  switch(fuel)
  {
    case E10_87:
      return FUEL_SALES[E10_87] += money;
    case E10_90:
      return FUEL_SALES[E10_90] += money;
    case DIESEL:
      return FUEL_SALES[DIESEL] += money;
  }
}


float accumulate_litres()
{
  return TOTAL_LITRES += litre();
}

float accumulate_litres2()
{
  return TOTAL_LITRES += payment_litre;
}

float convert_gallon_to_litres(float x)
{
  return x * 3.785;
}

//Converts the refuel_amount into gallons based on the fuel types
float gallon()
{
  switch (fuel)
    {
    case E10_87: return refuel_amount / 165.64;
		case E10_90: return refuel_amount / 171.74;
		case DIESEL: return refuel_amount / 159.38;
    }
}

float gct()
{
    return lub_price[lub] * 0.16;
}

float litre()
{
    switch (fuel)
    {
    case E10_87: return money / 184.9;
		case E10_90: return money / 193.6;
		case DIESEL: return money / 182.3;
    }
}


//Validates user to grant access to edit charge customer or view sales
int login() {
	const char *PASSWORD = "bruh";
	char input[51];
	scanf("%s", input);
	
	return !strcmp(input, PASSWORD);
}



int search_id (ChargeCustomer *client, int key)
{
    for (int i = 0; i < SIZE; i++) 
    {
        if (client[i].id == key)
        {
            return i; 
        }
    }
    return -1;
}

int search_reps(ChargeCustomer *client, int key)
{
    for (int i = 0; i < SIZE; i++) 
    {
        if (client[i].representatives == key)
        {
            return i; 
        }
    }
    return -1;
}

void add_charge_customer(ChargeCustomer *ptrclient)
{
    printf("Enter admin password: ");
    if (!login()) {
		printf("Incorrect password\n");
    }
    else
    {
        puts("Login successful");
        printf("New customer has been automatically assigned to id %d\n",current_charge_id);
        ptrclient[chargelist].id = current_charge_id;
        printf("Enter business name: ");
        scanf("%s", ptrclient[chargelist].name);
        prompt_int_range("Enter the number of representatives",  &reps, 1, 5, "Number must be from 1 to 5");
        ptrclient[chargelist].representatives = reps;
		    for (int i = 0; i < reps; i += 1) 
		    {
			    generate_license(ptrclient,i);
		    }
        generate_preference_output(ptrclient);
        if (ptrclient[current_customer].preference_number == DEPOSIT)
        {
          printf("Enter the initial money: $");
          scanf("%f",&ptrclient[current_customer].initial_money);
          while (ptrclient[current_customer].initial_money < min_deposit)
          {
            printf("The minimum deposit is $%.2f\n",min_deposit);
            printf("Enter the initial money: $");
            scanf("%f",&ptrclient[current_customer].initial_money);
          }
        }
        else if(ptrclient[current_customer].preference_number == MAXIMUM)
        {
          printf("Enter the initial litres: ");
          scanf("%f",&ptrclient[current_customer].initial_litres);
          while (ptrclient[current_customer].initial_litres > max_litres)
          {
            printf("The maximum litres is %.2f\n", max_litres);
            printf("Enter the initial litres: ");
            scanf("%f",&ptrclient[current_customer].initial_litres);
          }
        }
        puts("New customer has been successfully added to the system");
        chargelist++;
        current_charge_id++;
    }
}

void create_default_customers(ChargeCustomer *ptrclient) {
	ChargeCustomer DEFAULT[3] = {
		{ 1, "TANKWELDLTD", {"5786KW","0578PQ","7777TY"},3,"N/A","DEPOSIT","N/A", 0, 0, DEPOSIT, 0, 100000, 100000, 0, 0, 0, 0, 0, 0, 0},
		{ 2, "LEADINGEDGELTD", {"6588HH", "5436RK"}, 2, "N/A", "MAXIMUM", "N/A" , 0, 0, MAXIMUM, 0, 0, 0, 0, 50, 50, 0, 0, 0, 0},
		{ 3, "DERRIMONTRADINGLTD", {"3378JQ"}, 1, "N/A", "DEPOSIT", "N/A", 0, 0, DEPOSIT, 0, 50000, 50000, 0, 0, 0, 0, 0, 0, 0}
	};
	ptrclient[0] = DEFAULT[0];
	ptrclient[1] = DEFAULT[1];
	ptrclient[2] = DEFAULT[2];
}

void deposit_serve(ChargeCustomer *ptrclient)
{   puts("Serving Preference Deposit");
    prompt_int_range("Enter fuel type (E10—87 = 1, E10-90 = 2, Diesel = 3)", &fuel, 1, 3, NULL);
    strcpy(ptrclient[current_customer].fuel_type,fuel_types[fuel]);
    printf("Current Deposit Amount: $%.2f\n",ptrclient[current_customer].current_money);
    printf("Enter the amount of fuel needed or Press 0 to Exit: $");
	  scanf("%f", &money);
	  while(ptrclient[current_customer].current_money - money < 0 ||  CURRENT_FUEL_TANK_CAPACITY[fuel] - litre() < 0)
	    {
	       printf("Money entered has either exceeded Current deposit amount or Current Tank Capactity\n");
	       printf("Enter a lower amount or Press 0 to Exit");
	       scanf("%f",&money);
	    }
	    accumulate_fuel_sales();
		  accumulate_litres();
		  CURRENT_FUEL_TANK_CAPACITY[fuel] -= litre();
	    ptrclient[current_customer].current_money -= money;
	    item_count = 1;
	  	ptrclient[current_customer].fuel_amount = money;
	  	ptrclient[current_customer].money = ptrclient[current_customer].fuel_amount;
	  	int response = lub_req();
	   printf("Lubricant Request? %c\n", response);
		//initialises lub to 0 once the loop starts again to not cause errors
		ptrclient[current_customer].lubricant_amount = lub_price[0];
		if (response == 'Y') {
			prompt_int_range("Enter the lubricant type (5W-30 = 1, 5W-40 – 2, 15W-40 – 3, SAE – 40 - 4)", &lub, 1, 4, NULL);
			strcpy(ptrclient[current_customer].lubricant,lubricant_types[lub]);
			while (1) 
			{
			  printf("Enter the lubricant amount or Press 0 to Exit: $");
				scanf("%f",&ptrclient[current_customer].lubricant_amount);
				while(ptrclient[current_customer].current_money - ptrclient[current_customer].lubricant_amount < 0)
	      {
	        printf("Money has exceeded Current deposit amount\n");
	        printf("Enter a lower amount or Press 0 to Exit");
	        scanf("%f",&ptrclient[current_customer].lubricant_amount);
	      }
				if(ptrclient[current_customer].lubricant_amount >= lub_price[lub] || ptrclient[current_customer].lubricant_amount == 0)
				    break;
				else
				    printf("Invalid. Please enter a higher amount than $%.2f\n",ptrclient[current_customer].lubricant_amount);
			}
			ptrclient[current_customer].current_money -= ptrclient[current_customer].lubricant_amount;
			ptrclient[current_customer].money += ptrclient[current_customer].lubricant_amount;
			//lubricant amount gets reassigned to its rightful value
			ptrclient[current_customer].lubricant_amount = lub_price[lub];
			ptrclient[current_customer].gct_amount = gct();
			item_count += 1;
		}	
		else
		{
		    strcpy(ptrclient[current_customer].lubricant,lubricant_types[lub]);
		}
		ptrclient[current_customer].sub_total = ptrclient[current_customer].fuel_amount + ptrclient[current_customer].lubricant_amount;
		ptrclient[current_customer].grand_total = ptrclient[current_customer].sub_total + ptrclient[current_customer].gct_amount;
		SALES_GRAND_TOTAL[CHARGE] += ptrclient[current_customer].grand_total;
		ptrclient[current_customer].change = ptrclient[current_customer].money - ptrclient[current_customer].grand_total;
		receipt2(ptrclient);
		chargecount++;
}

void generate_license(ChargeCustomer *ptrclient, int i)
{
    char string[20];
    for (int i = 0; i < 4; i++)
    {
      string[i] = 48 + (rand() % 57);
      while (string[i] <48 || string[i] > 57)
      {
        string[i] = 48 + (rand() % 57);
      }
    }
    
    for (int i = 4; i <6; i++)
    {
      string[i] = 65 + (rand() % 90);
      while (string[i] <65 || string[i] > 90)
      {
        string[i] = 65 + (rand() % 90);
      }
    }
    strcpy(ptrclient[chargelist].licenses[i],string);
    printf("%s has been assigned to license number %d\n",string,i + 1);
}

void generate_report(ChargeCustomer *ptrclient)
{
  printf("Enter admin password: ");
    if (!login()) {
		printf("Incorrect password\n");
    }
    else
    {
        puts("Login successful");
        prompt_int_range("Which report would you like to view? (1 = Sales report, 2 = Charge Customers report, 3 = Fuel report)", &report_option, 1, 3, NULL);
        puts("");
        switch (report_option)
        {
          case SALES_REPORT:
            puts("Stateline Gas Station Sales Report");
            printf("Total Cash Customers: %d\n",cashcount);
            printf("Total Charge Customers: %d\n", chargecount);
            printf("Total Cash Amount: $%.2f\n", SALES_GRAND_TOTAL[CASH]);
            printf("Total Charge Amount: $%.2f\n",SALES_GRAND_TOTAL[CHARGE]);
            printf("Grand Total: $%.2f\n", SALES_GRAND_TOTAL[CASH] + SALES_GRAND_TOTAL[CHARGE]);
            break;
          case CHARGE_REPORT:
            puts("Stateline Gas Station Charge Report");
            for (int i = 0; i < 3; i++)
            {
              printf("Customer id: %d\n", ptrclient[i].id);
              printf("Customer name: %s\n", ptrclient[i].name);
              printf("Initial Deposit Amount: $%.2f\n",ptrclient[i].initial_money);
              printf("Balance Remaining: $%.2f\n", ptrclient[i].initial_money - ptrclient[i].money);
              printf("Initial Litres Amount: %.2f\n", ptrclient[i].initial_litres);
              printf("Litres Remaining: %.2f\n", ptrclient[i].initial_litres - ptrclient[i].litres);
              printf("Amount Owned: \n");
              printf("Amount Paid: \n");
              printf("Balance Remaining: \n");
              puts("");
            }
            break;
          case FUEL_REPORT:
            puts("Stateline Gas Station Fuel Report");
            printf("Total Fuel Sales: $%.2f\n",FUEL_SALES[E10_87] + FUEL_SALES[E10_90] + FUEL_SALES[DIESEL]);
            printf("E10-87 Sales: $%.2f\n", FUEL_SALES[E10_87]);
						printf("E10-90 Sales: $%.2f\n", FUEL_SALES[E10_90]);
						printf("Diesel Sales: $%.2f\n", FUEL_SALES[DIESEL]);
						printf("Total Litres Purchased: %.2f litres\n", TOTAL_LITRES);
            break;
            
        }
    }
}

void maximum_litre_serve(ChargeCustomer *ptrclient)
{
    puts("Serving Preference Maximum Litres");
    prompt_int_range("Enter fuel type (E10—87 = 1, E10-90 = 2, Diesel = 3)", &fuel, 1, 3, NULL);
    strcpy(ptrclient[current_customer].fuel_type,fuel_types[fuel]);
    printf("Current Litres Amount: %.2f\n",ptrclient[current_customer].current_litres);
    printf("Enter the amount of litres needed: ");
	  scanf("%f", &payment_litre);
	  while(ptrclient[current_customer].current_litres - payment_litre < 0 || payment_litre < 1 || payment_litre > CURRENT_FUEL_TANK_CAPACITY[fuel])
	    {
	       printf("Litre has either exceeded or not meet above 0 litres\n");
	       printf("Enter amount of litres: ");
	       scanf("%f",&payment_litre);
	    }
	   accumulate_litres2();
	   accumulate_fuel_sales2();
	   CURRENT_FUEL_TANK_CAPACITY[fuel] -= payment_litre;
	   ptrclient[current_customer].current_litres -= payment_litre;
	   item_count = 1;
	   ptrclient[current_customer].fuel_amount = payment_litre * fuel_per_litre[fuel];
	   ptrclient[current_customer].money = payment_litre * fuel_per_litre[fuel];
	   int response = lub_req();
	   printf("Lubricant Request? %c\n", response);
		//initialises lub to 0 once the loop starts again to not cause errors
		ptrclient[current_customer].lubricant_amount = lub_price[0];
		if (response == 'Y') {
			prompt_int_range("Enter the lubricant type (5W-30 = 1, 5W-40 – 2, 15W-40 – 3, SAE – 40 - 4)", &lub, 1, 4, NULL);
			strcpy(ptrclient[current_customer].lubricant,lubricant_types[lub]);
			while (1) 
			{
			  printf("Enter the lubricant amount: ");
				scanf("%f",&payment_litre);
				while(ptrclient[current_customer].current_litres - payment_litre < 0 || payment_litre < 1)
	      {
	        printf("Litre entered either has exceeded current litres in account or less than Mimimum litre\n");
	        printf("Enter a lower amount or Press 0 to Exit: ");
	        scanf("%f",&payment_litre);
	      }
				if(payment_litre * lub_price[lub] >= lub_price[lub])
				    break;
				else
				    puts("Invalid");
			}
			ptrclient[current_customer].current_litres -= payment_litre;
			ptrclient[current_customer].money += payment_litre * lub_price[lub];
			//lubricant amount gets reassigned to its rightful value
			ptrclient[current_customer].lubricant_amount = lub_price[lub];
			ptrclient[current_customer].gct_amount = gct();
			item_count += 1;
		}	
		else
		{
		    strcpy(ptrclient[current_customer].lubricant,lubricant_types[lub]);
		}
		ptrclient[current_customer].sub_total = ptrclient[current_customer].fuel_amount + ptrclient[current_customer].lubricant_amount;
		ptrclient[current_customer].grand_total = ptrclient[current_customer].sub_total + ptrclient[current_customer].gct_amount;
		SALES_GRAND_TOTAL[CHARGE] += ptrclient[current_customer].grand_total;
		ptrclient[current_customer].change = ptrclient[current_customer].money - ptrclient[current_customer].grand_total;
		receipt2(ptrclient);
		chargecount++;
	   
}

void payment_charge_customer(ChargeCustomer *ptrclient)
{
    printf("Enter admin password: ");
    if (!login()) {
		printf("Incorrect password\n");
    }
    else
    {
        puts("Login successful");
        printf("Enter customer id to make payment: ");
        scanf("%d",&id);
        if (search_id(ptrclient,id) != -1)
        {
            puts("Customer has been found");
            current_customer = search_id(ptrclient,id);
            if (ptrclient[current_customer].preference_number == DEPOSIT)
            {
              puts("Preference Type: Deposit");
              prompt_int_range("Enter payment type (Cash/Card = 1 or Cheque = 2)",&type_pay,1, 2, NULL);
              printf("Enter payment amount or Press 0 to Exit: ");
              scanf("%f",&payment);
              while (payment < min_money_card && type_pay == CARDCASH)
              {
                if (payment == 0)
                {
                  break;
                }
                printf("The Mimimum payment cash/card amount is $%.2f\n",min_money_card);
			          printf("Enter payment amount  or Press 0 to exit: $");
			          scanf("%f",&payment);
              }
              while(payment < min_cheque && type_pay == CHEQUE)
              {
                if (payment == 0)
                {
                  break;
                }
                printf("The Mimimum payment cash/card amount is $%.2f\n",min_cheque);
			          printf("Enter payment amount or Press 0 to exit: $");
			          scanf("%f",&payment);
              }
                ptrclient[current_customer].current_money += payment;
            }
            else if (ptrclient[current_customer].preference_number == MAXIMUM)
            {
              printf("Enter the litres needed: ");
              scanf("%f",&payment_litre);
              while(payment_litre > max_litres)
              {
                printf("The max litres is %.2f\n",max_litres);
                printf("Enter the litres needed: ");
                scanf("%f",&payment_litre);
              }
              ptrclient[current_customer].current_litres += payment_litre;
            }
        else
        {
            puts("Invalid id. Customer was not found");
        }
    }
  }
}


void prompt_int_range(const char *message, int *option, int min, int max, const char *error) {
	while (1) {
		printf("%s: ", message);
		scanf("%d", option);
		if (*option >= min && *option <= max)
			break;
		else if (error != NULL)
			printf("%s\n", error);
		else
				printf("Invalid option\n");
	}
}

void receipt1(Customer *ptrcust)
{
	puts("");
	puts("Stateline Gas Station");
	printf("Date of transaction: %s\n", get_current_date());
	printf("Customer Type: %s\n", ptrcust[serve_list].cust_type);
	printf("Item count: %d\n",item_count);
	printf("===============================\n");
	printf("Fuel Type: %s\n",ptrcust[serve_list].fuel_type);
	printf("Cost: $%.2f\n",ptrcust[serve_list].fuel_amount);
	printf("Lubricant Type: %s\n",ptrcust[serve_list].lubricant);
	printf("Cost: $%.2f\n",ptrcust[serve_list].lubricant_amount);
	printf("===============================\n");
	printf("Sub-Total: $%.2f\n",ptrcust[serve_list].sub_total);
	printf("GCT: $%.2f\n",ptrcust[serve_list].gct_amount);
	printf("Grand Total: $%.2f\n\n",ptrcust[serve_list].grand_total);
	printf("Cash: $%.2f\n",ptrcust[serve_list].grand_total);
	printf("Amount Tendered: $%.2f\n",ptrcust[serve_list].money);
	printf("Change/Amount Owned: $%.2f\n",ptrcust[serve_list].change);
}

void receipt2(ChargeCustomer *ptrclient)
{
  puts("");
	puts("Stateline Gas Station");
	printf("Date of transaction: %s\n", get_current_date());
	printf("Customer Type: Charge\n");
	printf("Item count: %d\n",item_count);
	printf("===============================\n");
	printf("Fuel Type: %s\n",ptrclient[current_customer].fuel_type);
	printf("Cost: $%.2f\n",ptrclient[current_customer].fuel_amount);
	printf("Lubricant Type: %s\n",ptrclient[current_customer].lubricant);
	printf("Cost: $%.2f\n",ptrclient[current_customer].lubricant_amount);
	printf("===============================\n");
	printf("Sub-Total: $%.2f\n",ptrclient[current_customer].sub_total);
	printf("GCT: $%.2f\n",ptrclient[current_customer].gct_amount);
	printf("Grand Total: $%.2f\n\n",ptrclient[current_customer].grand_total);
	printf("Cash: $%.2f\n",ptrclient[current_customer].grand_total);
	printf("Amount Tendered: $%.2f\n",ptrclient[current_customer].money);
	printf("Change/Amount Owned: $%.2f\n",ptrclient[current_customer].change);
}



void refuel_tank()
{
   printf("Enter admin password: ");
   if (!login()) {
     printf("Incorrect password\n");
    }
    else
    {
        puts("Login successful");
        prompt_int_range("Enter fuel type (E10—87 = 1, E10-90 = 2, Diesel = 3)", &fuel, 1, 3, NULL);
        switch (fuel)
        {
          case E10_87:
            refuel_tank_output();
            break;
          case E10_90:
            refuel_tank_output();
            break;
          case DIESEL:
            refuel_tank_output();
            break;
        }
        
    }
}

void refuel_tank_output()
{
    printf("Current Tank Capacity: %.2f litres\n",CURRENT_FUEL_TANK_CAPACITY[fuel]);
    printf("Enter the refuel amount in gallons or Press 0 to exit: ");
    scanf("%f",&refuel_amount);
    while (CURRENT_FUEL_TANK_CAPACITY[fuel] + convert_gallon_to_litres((gallon())) > FUEL_TANK_CAPACITY[fuel] || refuel_amount < refuel_per_gallon[fuel]) 
    {
      if(refuel_amount == 0)
			{
			  break;
			}
		  printf("Higher than $%.2f is required.\n",refuel_per_gallon[fuel] *2);
			printf("Enter refuel amount in gallons or Press 0 to exit: ");
			scanf("%f",&refuel_amount);
		}
		CURRENT_FUEL_TANK_CAPACITY[fuel] += convert_gallon_to_litres(gallon());
		puts("Tank has been successfully refueled");
		printf("Current Tank Capacity: %.2f litres\n", CURRENT_FUEL_TANK_CAPACITY[fuel]);
}

void remove_charge_customer(ChargeCustomer *ptrclient)
{
    printf("Enter admin password: ");
    if (!login()) {
		printf("Incorrect password\n");
    }
    else
    {
        puts("Login successful");
        printf("Enter customer id number to delete: ");
        scanf("%d",&id);
        if (search_id(ptrclient,id) != -1)
        {

            puts("Customer has been found");
            current_customer = search_id(ptrclient,id);
            ptrclient[current_customer] = (ChargeCustomer) {
            .id = 0,
            .licenses = {0},
            .representatives = 0,
            .fuel_type = {0},
            .preference = {0},
            .lubricant = {0},
            .lubricant_amount = 0,
            .fuel_amount = 0,
            .preference_number = 0,
            .money = 0,
            .current_money = 0,
            .initial_money = 0,
            .litres = 0,
            .current_litres = 0,
            .initial_litres = 0,
            .gct_amount = 0,
            .sub_total = 0,
            .grand_total = 0,
            .change = 0
            };
            puts("Customer fields has been deleted from system");
        }
        else
        {
            puts("Invalid id. Customer was not found");
        }
    }
}

void serve_customer(Customer *ptrcust, ChargeCustomer *ptrclient)
{
    char input[30];
    item_count = 0;
    prompt_int_range("Enter a customer type (1 - Cash, 2 - Charge)", &cust_type, 1, 2, NULL);
    if (cust_type == CASH)
    {
        strcpy(ptrcust[serve_list].cust_type,"Cash");
        ptrcust[serve_list].gct_amount = 0;
		prompt_int_range("Enter the payment type (1 - Cash or 2 - Card)", &cod_type, 1, 2, NULL);
		prompt_int_range("Enter fuel type (E10—87 = 1, E10-90 = 2, Diesel = 3)", &fuel, 1, 3, NULL);
		strcpy(ptrcust[serve_list].fuel_type,fuel_types[fuel]);
		printf("Enter the amount of fuel needed: $");
		scanf("%f", &money);
		while (cod_type == 1 &&  litre() <min_litre_cash || litre() > CURRENT_FUEL_TANK_CAPACITY[fuel]) {
		    puts("");
		    if(litre() > CURRENT_FUEL_TANK_CAPACITY[fuel])
		    {
		      printf("Amount entered exteeds %s current tank capacity\n",fuel_types[fuel]);
		    }
		    printf("Mimimum of higher than $%.2f is required.\n",fuel_per_litre[fuel] *2);
			  printf("A minimum of 2 litres is required.\nPlease enter money or Press 0 to Exit: $");
			  scanf("%f",&money);
			  if(money == 0)
		    {
		      break;
		    }
		}
		
		while (cod_type == 2 && (money < min_money_card || litre() > CURRENT_FUEL_TANK_CAPACITY[fuel])) 
		{
		puts("");
		 if(money == 0)
		    {
		      break;
		    }
		if(litre() > CURRENT_FUEL_TANK_CAPACITY[fuel])
		{
		  printf("Amount entered exteeds %s current tank capacity\n",fuel_types[fuel]);
		}
		  printf("The minimum amount of money is $1000. Please enter money or Press 0 to Exit: $");
		  scanf("%f",&money);
		 
		  }
		accumulate_fuel_sales();
		accumulate_litres();
		CURRENT_FUEL_TANK_CAPACITY[fuel] -= litre();
	  item_count = 1;
		ptrcust[serve_list].fuel_amount = money;
		ptrcust[serve_list].money += ptrcust[serve_list].fuel_amount; 
		int response = lub_req();
        //Randomly generates yes or no
		printf("Lubricant Request? %c\n", response);
		//initialises lub to 0 once the loop starts again to not cause errors
		ptrcust[serve_list].lubricant_amount = lub_price[0];
		if (response == 'Y') {
			prompt_int_range("Enter the lubricant type (5W-30 = 1, 5W-40 – 2, 15W-40 – 3, SAE – 40 - 4)", &lub, 1, 4, NULL);
			strcpy(ptrcust[serve_list].lubricant,lubricant_types[lub]);
			while (1) 
			{
			  printf("Enter the lubricant amount: $");
				scanf("%f",&ptrcust[serve_list].lubricant_amount);
				if(ptrcust[serve_list].lubricant_amount >= lub_price[lub])
				    break;
				else
				    printf("Invalid. Please enter a higher amount than $%.2f\n",ptrcust[serve_list].lubricant_amount);
			}
			ptrcust[serve_list].money += ptrcust[serve_list].lubricant_amount;
			//lubricant amount gets reassigned to its rightful value
			ptrcust[serve_list].lubricant_amount = lub_price[lub];
			ptrcust[serve_list].gct_amount = gct();
			item_count += 1;
		}	
		else
		{
		    strcpy(ptrcust[serve_list].lubricant,lubricant_types[lub]);
		}
		ptrcust[serve_list].sub_total = ptrcust[serve_list].fuel_amount + ptrcust[serve_list].lubricant_amount;
		ptrcust[serve_list].grand_total = ptrcust[serve_list].sub_total + ptrcust[serve_list].gct_amount;
		SALES_GRAND_TOTAL[CASH] += ptrcust[serve_list].grand_total;
		ptrcust[serve_list].change = ptrcust[serve_list].money - ptrcust[serve_list].grand_total;
		receipt1(ptrcust);
		serve_list++;
		cashcount++;
		overall_list++;
    }
    else
    {
        if (cust_type == CHARGE)
        {
            printf("Please enter customer id: ");
            scanf("%d",&id);
            
            if (search_id(ptrclient,id) != -1)
            {
                current_customer = search_id(ptrclient,id);
                puts("Customer has been found");
                printf("Enter number of representatives: ");
                scanf("%d",&reps);
                if (search_reps(ptrclient,reps) !=-1 )
                {
                    puts("Number of representatives has been confirmed");
                    for (int j = 0; j < reps ; j++)
                    {
                        printf("Enter license number %d: ",j+1);
                        scanf("%s",license);
                        while (strcmp(license,ptrclient[current_customer].licenses[j])!=0)
                        {
                            printf("Invalid license number %d\n",j+1);
                            printf("Enter correct license number: ");
                            scanf("%s",license);
                        }
                    }
                    
                    if(ptrclient[current_customer].preference_number == DEPOSIT)
                    {
                        deposit_serve(ptrclient);
                    }
                    else if(ptrclient[current_customer].preference_number == MAXIMUM)
                    {
                        maximum_litre_serve(ptrclient);
                    }
                    overall_list++;
	    	  }
                else
                {
                    puts("Number of representatives does not match the system records\n"
                        "Re-enter and try again");
                }
            }
            else
            {
                puts("Customer not found");
            }
        }
    }
}
    

void update_charge_customer(ChargeCustomer *ptrclient)
{
    printf("Enter admin password: ");
    if (!login()) {
		printf("Incorrect password\n");
    }
    else
    {
        puts("Login successful");
        printf("Enter customer id number to update: ");
        scanf("%d",&id);
        if (search_id(ptrclient,id) != -1)
        {
            current_customer = search_id(ptrclient,id);
            puts("Customer has been found");
            prompt_int_range("Which field would you like to edit?\n1 - All fields\n2 - Single field\nEnter option", &field_option, 1,2,NULL);
            switch(field_option)
            {
              case 1:
                printf("Input new business name of customer: ");
                scanf("%s",ptrclient[current_customer].name);
                prompt_int_range("Enter number of representatives: ", &reps, 1, 5, NULL);
                ptrclient[current_customer].representatives = reps;
                generate_preference_output(ptrclient);
                puts("Customer field has been successfully edited");
                break;
              case 2:
                  prompt_int_range("1 - Customer name\n2 - Number of representatives\n3-Preference\nEnter a single field to edit", &field_type, 1 ,3, NULL );
                  if (field_type == 1)
                  {
                    printf("Enter new business name: ");
                    scanf("%s",ptrclient[current_customer].name);
                  }
                  else
                  {
                    if(field_type == 2)
                    {
                      prompt_int_range("Enter new number of representatives (1 - 5): ",&ptrclient[current_customer].representatives, 1, 5, NULL);
                    }
                    else
                    {
                      generate_preference_output(ptrclient);
                    }
                  }
                  puts("Customer field has been successfully edited");
                  break;
            }
        }
        else
        {
            puts("Invalid ID. Customer not found");
        }
    }
}

void saveToFileCash(FILE *fcashcust, Customer *ptrcust) {
    for (int i = 0; i < cashcount; i++) {
        fprintf(fcashcust, "%5s %9s %9s %12.2f %5.2f %12.2f %12.2f %12.2f\n",
        ptrcust->cust_type, ptrcust->fuel_type, ptrcust->lubricant, ptrcust->sub_total, ptrcust->gct_amount, 
        ptrcust->grand_total, ptrcust->money, ptrcust->change);
        ptrcust++;
    }
    fclose(fcashcust);
}
void saveToFileCharge(FILE *fchargecust, ChargeCustomer *ptrclient) {
   fprintf(fchargecust, "%4s %20s %4s %10s %12s %10s\n","ID","Customer Name","Reps","Preference","Amount $", "Litre");
    for (int i = 0; i < chargelist; i++) {
        fprintf(fchargecust, "%4d %20s %4d %10s %12.2f %10.2f\n",
        ptrclient->id, ptrclient->name, ptrclient->representatives, ptrclient->preference,
        ptrclient->current_money, ptrclient->current_litres);
        ptrclient++;
    }
    fclose(fchargecust);
}

void saveToFileCharge2(FILE *fchargecust2, ChargeCustomer *ptrclient) {
    fprintf(fchargecust2,"%4s %6s %6s %6s %6s %6s\n", "ID", "Rep#1", "Rep#2", "Rep#3", "Rep#4", "Rep#5");
    for (int i = 0; i < chargelist; i++)
    {
      fprintf(fchargecust2,"%4d %6s %6s %6s %6s %6s\n", ptrclient[i].id,
      ptrclient[i].licenses[0], ptrclient[i].licenses[1],ptrclient[i].licenses[2], ptrclient[i].licenses[3], ptrclient[i].licenses[4]);
    }

    fclose(fchargecust2);
}
