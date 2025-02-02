#include <iostream>
#include <fstream>
#include <string>
#include <windows.h>
using namespace std;
//only for techders view all student records 
void ViewAllRecords() {
	
	string name, reg, course, contact, email;
	system("cls");
	cout<<"System takes some time to show the records please be patient "<<endl;
	Sleep(5000);
	system("cls");

    ifstream inFile("student.txt"); 

    cout << "\n--- All Student Records ---\n" << endl;

    while (getline(inFile, name, ',') && 
           getline(inFile, reg, ',') && 
           getline(inFile, course, ',') && 
           getline(inFile, contact, ',') && 
           getline(inFile, email)) 
    {
    
        cout << "\nStudent Record:\n";
        cout << "Name: " << name << endl;
        cout << "Registration Number: " << reg << endl;
        cout << "Course: " << course << endl;
        cout << "Contact: " << contact << endl;
        cout << "Email: " << email << endl;
        cout << "-------------------------" << endl;
    }

    inFile.close();

    
}


//students record system functions
void AddRecord() {
	system("cls");
	ofstream inFile("student.txt", ios::app);
	string name, reg, course, contact, email;
    cin.ignore();
    
  	cout<<"Enter you name :"<<endl;
   	getline(cin, name);
   	cout<<"Enter your Registration Number :"<<endl;
   	getline(cin, reg);
   	cout<<"Enter your Course : "<<endl;
   	getline(cin, course);
   	cout<<"Enter your Contact Number : "<<endl;
    getline(cin, contact);
    cout<<"Enter you E-mainl Address"<<endl;
    getline(cin, email);
    inFile <<"RECORDS,"<<name<<","<<reg<<","<<course<<","<<contact<<","<<email<<endl;
    inFile.close(); 
    cout<<"Records Added Successfuly ! "<<endl;
    
}

void SearchRecord() {
	system("cls");
	ifstream inFile("student.txt", ios::app);
	string type, name, reg, course, contact, email;
    cin.ignore();
    
    string searchReg;
    bool found = false;
    
    cout<<"Enter your Registration Number : ";
    getline(cin, searchReg);
    
    while (getline(inFile, type, ',') && 
    	getline(inFile, name, ',') &&
        getline(inFile, reg, ',') && 
        getline(inFile, course, ',') && 
        getline(inFile, contact, ',') && 
        getline(inFile, email))
    {
    	if (type == "RECORDS" && reg == searchReg) {
            found = true;
            cout << "\n--- Student Record Found ---\n";
            cout << "Name: " << name << endl;
            cout << "Registration Number: " << reg << endl;
            cout << "Course: " << course << endl;
            cout << "Contact: " << contact << endl;
            cout << "Email: " << email << endl;
            break; 
        }
	}
    if (!found) {
        cout << "No record found for Registration Number: " << searchReg << endl;
    }
    inFile.close();
    
}

void UpdateRecord() {
    system("cls");
    ifstream inFile("student.txt"); 
    if (!inFile) {
        cout << "Error opening file!" << endl;
        return;
    }

    ofstream tempFile("temp.txt"); 
    if (!tempFile) {
        cout << "Error creating temp file!" << endl;
        return;
    }

    string name, reg, course, contact, email;
    string searchReg;
    bool found = false;

    cin.ignore();
    cout << "Enter your Registration Number: ";
    getline(cin, searchReg);

    while (getline(inFile, name, ',') && 
           getline(inFile, reg, ',') && 
           getline(inFile, course, ',') && 
           getline(inFile, contact, ',') && 
           getline(inFile, email)) 
    {
        if (searchReg == reg) {
            found = true;
            cout << "\nStudent Found! Enter New Details:\n";

            cout << "Enter New Name: ";
            getline(cin, name);

            cout << "Enter New Course: ";
            getline(cin, course);

            cout << "Enter New Contact: ";
            getline(cin, contact);

            cout << "Enter New Email: ";
            getline(cin, email);

            tempFile << name << "," << reg << "," << course << "," << contact << "," << email << endl;
            cout << "\nRecord Updated Successfully!\n";
        } else {
            
            tempFile << name << "," << reg << "," << course << "," << contact << "," << email << endl;
        }
    }

    inFile.close();
    tempFile.close();

    if (!found) {
        cout << "Student with Registration No " << searchReg << " not found!" << endl;
        remove("temp.txt"); 
    } else {
        remove("student.txt");  // Delete the original file        
        rename("temp.txt", "student.txt"); // Rename the temporary file to the original file name
    }
}

void DeleteRecord() {
    ifstream inFile("student.txt");
    ofstream tempFile("temp.txt");
    cin.ignore();

    string name, registration, password, storeReg, storePass;
    bool found = false;

    cout << "Enter your Registration ID to delete your record: ";
    getline(cin, registration);

    cout << "Are you sure you want to delete your record? (yes/no): ";
    string confirm;
    getline(cin, confirm);

    if (confirm != "yes") {
        cout << "Deletion cancelled!" << endl;
        inFile.close();
        tempFile.close();
        return;
    }

    // Reading the file and copying all data except the record to be deleted
    while (getline(inFile, name, ',') && 
           getline(inFile, storeReg, ',') && 
           getline(inFile, storePass)) {
        if (storeReg != registration) {
            tempFile << name << " , " << storeReg << " , " << storePass << endl;
        } else {
            found = true;
        }
    }

    inFile.close();
    tempFile.close();

    if (!found) {
        cout << "Record with Registration ID " << registration << " not found!" << endl;
        return;
    }

    remove("student.txt"); // Delete the original file
    rename("temp.txt", "student.txt"); // Rename the temporary file to the original file name
    cout << "Record deleted successfully!" << endl;

}

void ViewRecord() {
	system("cls");
	ifstream inFile("student.txt", ios::app);
	string type, name, reg, course, contact, email;
    cin.ignore();
    
    string searchReg;
    bool found = false;
    
    cout<<"Enter your Registration Number : ";
    getline(cin, searchReg);
    
    while (getline(inFile, type, ',') && 
    	getline(inFile, name, ',') &&
        getline(inFile, reg, ',') && 
        getline(inFile, course, ',') && 
        getline(inFile, contact, ',') && 
        getline(inFile, email))
    {
    	if (type == "RECORDS" && reg == searchReg) {
            found = true;
            cout << "\n--- Student Record Found ---\n";
            cout << "Name: " << name << endl;
            cout << "Registration Number: " << reg << endl;
            cout << "Course: " << course << endl;
            cout << "Contact: " << contact << endl;
            cout << "Email: " << email << endl;
            break; 
        }
	}
    if (!found) {
        cout << "No record found for Registration Number: " << searchReg << endl;
    }
    inFile.close();
}

void GradCheck() {
	float avg ;
	int total_marks = 500;
	int sum;
	int english, urdu, maths, computer, physics;
	cout<<"\t\t\t\tEnter the marks of 5 subjects out of total 100 marks each\n\n";
	cout<<"Enter the marks of English\n";
	cin>>english;
	cout<<"Enter the marks of Urdu\n";
	cin>>urdu;
	cout<<"Enter the marks of Maths\n";
	cin>>maths;
	cout<<"Enter the marks of Computer\n";
	cin>>computer;
	cout<<"Enter the marks of Physics\n";
	cin>>physics;
	
	sum = english+maths+urdu+computer+physics;
	avg = (sum*100) / total_marks;
	cout<<avg;
	if(avg <= 100 && avg >= 85)
		{
			cout<<"Congrats you got 'A' grade :)";
		}
		else if(avg <= 85 && avg >= 75)
		{
			cout<<"You  achived 'B' grade  ";
	    }
	    else if(avg <= 75 && avg >= 65) {
	    	cout<<"You  achived 'C' grade  ";
		}
	    else if(avg <= 55 && avg >= 55) {
	    	cout<<"You  achived 'D' grade ";
		}
	    else if(avg <= 55 ) {
	    	cout<<"You  achived 'F' grade :( ";
		}
		else{
			cout<<"You might entered a invalid input !"<<endl;
		}
		
		if(avg <= 100 && avg >= 80) {
			cout<<"Congrats you got 100 % Scholarships "<<endl;
		}
		else {
			cout<<"You didn not got the scholarship "<<endl;
		}
	}

//student records ends here
//registration starts here for teachers 
void RegistrationTeacher() {
	system("cls");
	
	ofstream inFile("teacher.txt", ios::app);
	
	cin.ignore(); 
	string name, password, quez ;
	string ID;	
	cout<<"Enter you Full Name :";
	getline(cin, name);
	cout<<"Enter your Teacher ID :";
	getline(cin, ID);
	cout<<"Enter your Passwpord : ";
	getline(cin, password);
	inFile <<name<<","<<ID<<","<<password<<endl;
	inFile.close();
}

void LoginTeacher() { 
	
    system("cls");
    ifstream inFile("teacher.txt"); 
    T:
    bool found = false;
    cin.ignore();
    string registration, password;
    cout << "Enter your Registration ID: ";
    getline(cin, registration);
    cout << "Enter Password: ";
    getline(cin, password);

    string storeName, storeReg, storePass;

    while (getline(inFile, storeName, ',') &&  
           getline(inFile, storeReg, ',') && 
           getline(inFile, storePass )) 
		   {
        if (storeReg == registration && storePass == password) {
            found = true;
            inFile.close();
            cout << "\nLogin Successful!" << endl;
            system("cls");
            cout << "Please wait loading...." << endl;
            Sleep(2000);
            system("cls");
            Z:
            int choice;
            cout << "1. View All Students Records " << endl;
            cout << "2. Search Record" << endl;
            cout << "3. Exit" << endl;
            cin >> choice;
            
            if (choice == 1) {
                ViewAllRecords();
                goto Z;
            }
            else if (choice == 2) {
                SearchRecord();
                goto Z;
                
            }
            else if (choice == 3) {
                exit(0);
            }
            else {
                cout << "Invalid Input" << endl;
            }
            break;
        }
    }

    if (!found) {
        cout << "\nInvalid Registration ID or Password!" << endl;
        goto T;
    }	
}

//Registrations starst here for students
void RegistrationStudent() {
	system("cls");
	ofstream outFile("student.txt", ios::app);
	cin.ignore(); 
	
	string registration, name ,password, quez;
	
	cout<<"Enter your Full Name : ";
	getline(cin, name);
	cout<<"Enter your Registration ID : ";
	getline(cin, registration);
	cout<<"Enter Password : ";
	getline(cin, password);
	cout<<"Who is your favourait football player ? :- ";
	getline(cin, quez);
	outFile<<"LOGIN,"<<name<<","<<registration<<","<<password<<","<<quez<<endl;
	outFile.close();
	cout << "Registration successful!" << endl;
	  
}

void ResetPassStudents() {
	system("cls");
    ifstream inFile("student.txt");
    ofstream tempFile("temp.txt");
    cin.ignore();

    string name, registration, password, storeReg, storePass, inputAnswer, newPassword, storeQuez;
    bool found = false;

    cout << "Enter your Registration ID: ";
    getline(cin, registration);

    cout << "Who is your favourait FootBall Player : ";
    getline(cin, inputAnswer);

    while (getline(inFile, name, ',') && 
           getline(inFile, storeReg, ',') && 
           getline(inFile, storePass,',')&&
		   getline(inFile, storeQuez)) {
        
        if (storeReg == registration && storeQuez == inputAnswer) {
            found = true;

            cout << "Security question answered correctly!" << endl<<endl;
            cout << "Enter your new password: ";
            getline(cin, newPassword);

            tempFile<<name<<","<<registration<<","<<newPassword<<","<<storeQuez<<endl;
            cout << "Password updated successfully!" << endl;
            break;
        } else {
            tempFile<<name<<","<<registration<<","<<newPassword<<","<<storeQuez<< endl;

        }
    }

    inFile.close();
    tempFile.close();

    if (!found) {
        cout << "Error: Registration ID or Security Answer is incorrect." << endl;
        return;
    }

    remove("student.txt");
    rename("temp.txt", "student.txt");
}


void LoginStudent() {
	ifstream inFile("student.txt", ios::in);
	
	string registration, password;
    cout << "Enter your Registration ID: ";
    cin.ignore();
    getline(cin, registration);
    cout << "Enter Password: ";
    getline(cin, password);

    string type, storeName, storeReg, storePass, storeQuez;  
    bool loginSuccess = false;

    while (getline(inFile, type, ',') &&  
           getline(inFile, storeName, ',') &&
           getline(inFile, storeReg, ',') && 
           getline(inFile, storePass, ',')&&
		   getline(inFile, storeQuez))
		{
    	
    	if(type == "RECORDS" && storeReg == registration && storePass == password) {
    		
    		system("cls");
    		inFile.close();
    		cout<<"\t\t\t\tLogin Successfuly "<<endl<<endl;
    		Sleep(2000);
//    		system("cls");
    		cout<<"\t\t\t\tLoading please wait !"<<endl<<endl<<endl;
    		Sleep(2000);
    		system("cls");
    		
    	
    		D:
    		Sleep(2000);
    		system("cls");
    		int choice;
    		cout<<"-----------------------------------------------------------------------------------"<<endl<<endl;
    		cout<<"\t\t\t\t1 Add Records : "<<endl;
    		cout<<"\t\t\t\t2 Search Records : "<<endl;
    		cout<<"\t\t\t\t3 Update Records : "<<endl;
    		cout<<"\t\t\t\t4 Delete Records : "<<endl;
    		cout<<"\t\t\t\t5 View Records : "<<endl;
    		cout<<"\t\t\t\t6 Check Grades"<<endl;
    		cout<<"\t\t\t\t7 Log out : "<<endl;
    		cout<<"Enter your Choice: ";
    		cin>>choice;
    		switch(choice) {
    			case 1:
    				AddRecord();
    				goto D;
    				break;
    			
    			case 2:
    				SearchRecord();
    				int a;
    				cout<<"-------------------------------------------------------------------------"<<endl;
    				cout<<"\n\t\t\t0 exit !"<<endl;
    				cin>>a;
    				if(a == 0) {
    					goto D;	
					}
    				
    				break;
    				
    			case 3:
    				UpdateRecord();
    				int e;
    				cout<<"-------------------------------------------------------------------------"<<endl;
    				cout<<"\n\t\t\t0 exit !"<<endl;
    				cin>>e;
    				if(e == 0) {
    					goto D;	
					}
    				break;
    				
    			case 4:
    				DeleteRecord();
    				int b;
    				cout<<"-------------------------------------------------------------------------"<<endl;
    				cout<<"\n\t\t\t0 exit !"<<endl;
    				cin>>b;
    				if(b == 0) {
    					goto D;	
					}
    				break;
    				
    			case 5:
    				ViewRecord();
    				int c;
    				cout<<"-------------------------------------------------------------------------"<<endl;
    				cout<<"\n\t\t\t0 exit !"<<endl;
    				cin>>c;
    				if(c == 0) {
    					goto D;	
					}
    				break;
    		
    			case 6:
    				GradCheck();
    				int d;
    				cout<<"-------------------------------------------------------------------------"<<endl;
    				cout<<"\n\t\t\t0 exit !"<<endl;
    				cin>>d;
    				if(d == 0) {
    					goto D;	
					}
    				break;
    				
    			case 7:
    				Sleep(1000);
    				int f;
    				cout<<"-------------------------------------------------------------------------"<<endl;
    				cout<<"\n\t\t\t0 exit !"<<endl;
    				cin>>f;
    				if(f == 0) {
    					goto D;	
					}
    				break;
    				
    			default :
    				break;
			}//switch	
		}
		else {
			system("cls");
			cout<<"Your ID or password may be incorrect try again"<<endl<<endl;
			
		}	
	}  
}

int main() {
	system("cls");
	int choice;
	
	system("color 5b");
	cout<<"\t\t\t\t==================================================="<<endl;
	cout<<"\t\t\t\t|            Student Management System            |"<<endl; 
	cout<<"\t\t\t\t==================================================="<<endl<<endl;
	
	A:	
	system("cls");
	cout<<"\t\t\t\t1  Teacher "<<endl;
	cout<<"\t\t\t\t2  Student "<<endl<<endl;
	cout<<"\t\t\t\t3  Exit "<<endl<<endl;
	cout<<"Enter your choice ! "<<endl;
	cin>>choice;

	if(choice == 1) { int user;
		B:
		system("cls");
		cout<<"\t\t\t\t\t\tTeachers Registration and login !"<<endl<<endl;
		cout<<"\t\t\t\t1 Registration "<<endl;
		cout<<"\t\t\t\t2 Login "<<endl;
		cout<<"\t\t\t\t3 Exit <!> "<<endl;
		cout<<"Enter your choice !"<<endl;
		cin>>user;
		switch(user) {
			case 1:
				RegistrationTeacher();
				goto B;
				break;
				
			case 2:
				LoginTeacher();
				break;
				
			case 3:
				system("cls");
				cout<<"Thank you for using SMS :)"<<endl;
				goto A;
				
				break;
			default :
				cout<<"Invalid Input !"<<endl;
				break;
		}	
	}
	else if(choice == 2) { int user;
		C:
		system("cls");
		cout<<"\t\t\t\t\t\tStudents Registration and login !"<<endl<<endl;
		cout<<"\t\t\t\t1 Registration "<<endl;
		cout<<"\t\t\t\t2 Login "<<endl;
		cout<<"\t\t\t\t3 Re-Password "<<endl;
		cout<<"\t\t\t\t4 Exit <!> "<<endl;
		cout<<"Enter your choice !"<<endl;
		cin>>user;
		
		switch(user) {
			case 1:
				RegistrationStudent();
				goto C;
				break;
				
		    case 2:
		    	LoginStudent();
				break;
				
			case 3:
				ResetPassStudents();
				goto C;
				break;
			case 4:
				system("cls");
				cout<<"Thankyou for using SMS :)"<<endl;
				Sleep(3000);
				goto A;
				break;
			default :
				break;
		}
	}
	else if(choice == 3){
		exit(0);
	}
	else {
		system("cls");
		cout<<"Invalid Input !"<<endl<<endl;
		goto A;
		
	}
	
	
}
//123
