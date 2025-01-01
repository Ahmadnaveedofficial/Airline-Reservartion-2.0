#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>

using namespace std;

struct Flight
 {
    string flightNumber;
    string destination;
    string departureTime;
    string duration;
    float price;
};

struct Customer 
{
    int customerId;
    string name;
    int age;
    string gender;
    string address;
    string phone;
};

void inputCustomerDetails(Customer& customer) 
{          
    cout<<"\t\t\t\t\t\t\tEnter Customer ID: ";
    cin>> customer.customerId;
    cin.ignore();
    cout<<"\t\t\t\t\t\t\tEnter Name: ";
    getline(cin, customer.name);
    cout<<"\t\t\t\t\t\t\tEnter Age: ";
    cin>>customer.age;
    cin.ignore();
    cout<<"\t\t\t\t\t\t\tEnter Gender: ";
    getline(cin, customer.gender);
    cout<<"\t\t\t\t\t\t\tEnter Address: ";
    getline(cin, customer.address);
    cout<<"\t\t\t\t\t\t\tEnter Phone Number: ";
    getline(cin, customer.phone);
    cout<<"\n";
    cout<<"\t\t\t\t\t\t\tCustomer details saved successfully!" << endl;
}

void printTicket(int customerId, const Customer& customer, const Flight& flight) 
{
    ofstream outf("ticket.txt");
    if (outf.is_open())
	 {
        outf<<"<------------ Airline Ticket ------------>\n";
        outf<<"Customer ID:    \t"<<customer.customerId << endl;
        outf<<"Customer Name:  \t"<<customer.name << endl;
        outf<<"Customer Gender:\t"<<customer.gender << endl;
        outf<<"Flight Number:  \t"<<flight.flightNumber << endl;
        outf<<"Destination:    \t"<<flight.destination << endl;
        outf<<"Departure Time: \t"<<flight.departureTime << endl;
        outf<<"Duration:       \t"<<flight.duration << " hours" << endl;
        outf<<"Price:Rs.       \t"<<flight.price << endl;
    }
    outf.close();
    cout << "Ticket has been printed! Check 'ticket.txt'.\n";
}

void displayTicket(int customerId, const Customer& customer, const Flight& flight) 
{        

	cout<<"\n"<<endl;
    cout<<"\t\t\t\t\t\t\t <------------ Airline Ticket ------------>\n";
    cout<<"\t\t\t\t\t\t\t Customer ID:       "<<customer.customerId << endl;
    cout<<"\t\t\t\t\t\t\t Customer Name:     "<<customer.name<<endl;
    cout<<"\t\t\t\t\t\t\t Customer Gender:   "<<customer.gender<<endl;
    cout<<"\t\t\t\t\t\t\t Flight Number:     "<<flight.flightNumber<<endl;
    cout<<"\t\t\t\t\t\t\t Destination:      "<<flight.destination<<endl;
    cout<<"\t\t\t\t\t\t\t Departure Time:    "<<flight.departureTime<<endl;
    cout<<"\t\t\t\t\t\t\t Duration:          "<<flight.duration <<" hours"<< endl;
    cout<<"\t\t\t\t\t\t\t Price:             Rs."<<flight.price<<endl;
}

void initializeAndDisplayFlights(Flight flights[], int& flightCount)
 { 
 
flights[0] = {"Pk-498", "  Dubai", "08-12-2024 7:40PM", "04", 14000 }; 
flights[1] = {"Pk-198", "  Canada", "22-01-2024 5:40AM", "16", 34000 };
flights[2] = {"Pk-798", "  UK", "09-12-2024 7:40PM", "14", 44000 }; 
flights[3] = {"Pk-578", "  USA", "25-02-2024 5:40AM", "18", 94000 }; 
flights[4] = {"Pk-898", "  Australia", "22-01-2024 5:40AM", "16", 64000 }; 
flights[5] = {"Pk-348", "  Europe", "22-01-2024 5:40AM", "07", 78000 }; 
flightCount = 6; 


cout<<left<<setw(10)<<"Flight No"<<setw(15)<<"  Destination"
 <<setw(20)<<"  Departure"<<setw(10)<<"Duration\t"
 <<"Price"<<endl; 
for (int i = 0; i < flightCount; ++i) 
{ 
cout<<left<<setw(10)<<flights[i].flightNumber 
<<setw(15)<<flights[i].destination 
<<setw(20)<<flights[i].departureTime 
<<flights[i].duration<<setw(10)<<" hours" 
<<"Rs."<< flights[i].price << endl;
}

}



 
 void bookAndAddDetails(Customer& customer, Flight flights[], int flightCount, int& ticketId, bool& flightBooked, Flight& selectedFlight)
 {
 cout<<"\t\t\t\t\t\t\tSelect a flight by entering the flight number: ";
 
         string selectedFlightNumber; 
        cin>>selectedFlightNumber; 
         bool flightFound = false; 
for(int i = 0; i < flightCount; ++i)
 {
      if(flights[i].flightNumber == selectedFlightNumber)
      { 
            selectedFlight = flights[i]; 
			flightFound = true; 
			flightBooked = true;
	       break; 
      }
 }
 if(flightFound) 
      {
           cout<<"\n\t\t\t\t\t\t\tEnter Customer Details:\n\n";
               inputCustomerDetails(customer); 
             cout<<"\n\t\t\t\t\t\t\tFlight booked successfully!\n";
            displayTicket(ticketId++, customer, selectedFlight);
      }
      else
        { 
                cout<<"\n\t\t\t\t\t\t\tInvalid flight number! Please try again.\n";
        }
}


void printBookedTicket(int ticketId, bool flightBooked, const Customer& customer, const Flight& selectedFlight)
 { 
      if (flightBooked) 
    {
       cout<<"\n"; 
       printTicket(ticketId - 1, customer, selectedFlight);
    } 
       else 
    { 
       cout<<"\n\t\t\t\t\t\t\tNo ticket has been booked yet.\n"; 
    }
 }

void aboutUs()
 {
   
    cout<<"\n\n\n\n\n"
        <<"\t\t\t\t\t\t\t<------------------------- About Us ------------------------->\n"
        <<"\n\t\t\t\t\t\tWelcome to Pakistan International Airline, where your journey matters. \n"
        <<"\t\t\t\t\t\tExperience unmatched comfort and exceptional service on every flight.\n"
        <<"\n\t\t\t\t\tOur airline was founded by visionaries:\n"
        <<"\t\t\t\t\t\tAhmad with a passion for aviation and excellence. — \n"
        <<"\t\t\t\t\tWe are committed to providing a safe, efficient, and enjoyable travel experience.\n"
        <<"\n\t\t\t\t\t\t<----------------------------------------------------------->\n";
       
    }
        
        
void mainMenu()
 {

   int choice;
   int ticketId = 8989; 
   Customer customer; 
   Flight flights[10];
    int flightCount = 0; 
	initializeAndDisplayFlights(flights, flightCount); 
	Flight selectedFlight;
	 bool flightBooked = false;
    do 
	{
    	
        cout<<"\t\t\t\t\t\t\t                  " << endl;
        cout<<"\t\t\t\t\t\t\t  ---------------- Main Menu -----------------" << endl;
        cout<<"\t\t\t\t\t\t\t |\t\t\t\t\t      |" << endl;
        cout<<"\t\t\t\t\t\t\t |\t 1. View Available Flights            |" << endl;
        cout<<"\t\t\t\t\t\t\t |\t 2. Book a Flight                     |" << endl;
        cout<<"\t\t\t\t\t\t\t |\t 3. Print Ticket                      |" << endl;
        cout<<"\t\t\t\t\t\t\t |\t 4. What We Are?                      |" << endl;
        cout<<"\t\t\t\t\t\t\t |\t 5. Exit                              |" << endl;
        cout<<"\t\t\t\t\t\t\t |\t\t\t\t\t      |" << endl;
        cout<<"\t\t\t\t\t\t\t  --------------------------------------------\n" << endl;
        cout<<"Enter your choice: ";
        cin>>choice;
        cout<<"\n";

        switch(choice) 
		{
          case 1:
        	{
			
        	  cout<<"\t\t\t\t\t\t\tAvailable Flights:\n\n";
               initializeAndDisplayFlights (flights, flightCount);
            }
            break;
          case 2:
		    {    
		    bookAndAddDetails(customer,  flights,  flightCount,  ticketId, flightBooked,  selectedFlight);
		     }
            break;
       
        case 3:
        	{
           printBookedTicket( ticketId, flightBooked,  customer,  selectedFlight);
           	}
            break;
       case 4:
       	  {
       		aboutUs();
		   }
            	
            	break;
            	
        case 5:
        	{
        		cout<<"\t\t\t\t\t\t\tThank you for using Pakistan International Airline!\n";
			}
            
            break;
        default:
        {
        	 cout<<"\n\t\t\t\t\t\t\tInvalid choice! Please try again.\n";
		}
           
        }
        
        
    } while(choice != 5);
}


int main()
 {
 	  
    system("color F0"); 
    cout<<"\n\n\n\n";
cout<<"\t\t\t\t\t\t\t    Welcome to Pakistan International Airline  \n\n"<<endl; 
    mainMenu();
    
    return 0;
}
