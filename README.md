# iOS Developer Live Code

## Overview
This is a practical coding interview designed to assess your iOS development skills, particularly in clean architecture, MVVM pattern implementation, and UIKit proficiency.

**Duration:** 2 hours  
**Format:** Live coding session with screen sharing and camera on  
**Language:** Swift with UIKit (No SwiftUI, No Storyboards)

---

## Technical Requirements

### Folder Structure
Dashboard
- Controller
- ViewModel
- View
- Model

### Architecture: MVVM Pattern

Your application must follow the MVVM (Model-View-ViewModel) architecture with the following specifications:

#### ViewModel Structure
- ViewModel must be defined as a **protocol**
- All business logic must be implemented in a concrete class that conforms to this protocol
- The protocol should define all public methods and properties that the View Controller needs

#### Communication Pattern
- **MANDATORY:** Use the Delegate Pattern for ViewModel-to-View communication
- **PROHIBITED:** Do NOT use closures, callbacks, or completion handlers for ViewModel-to-View communication
- The ViewModel protocol should manage all interactions that the controller needs to observe
- The implementation class handles the actual business logic and notifies the delegate

Example structure:
```
protocol UserListViewModel {
    func fetchUsers()
}

protocol UserListViewModelDelegate: AnyObject {
    func didFetchUsers()
    func didFailWithError(_ error: Error)
    func reloadData()
}

final class UserListViewModelImpl: UserListViewModel {
    
}
```

### Network Layer

#### URLSession Implementation
- Use native **URLSession** for all network requests
- Implement a **generic request method** that can handle different response types
- Use **completion handlers** within the network layer for async operations
- **Only GET requests** will be used in this project

#### Generic Network Manager
Create a reusable network manager with a generic method structure:
```
func request<T: Decodable>(endpoint: String, 
                          completion: @escaping (Result<T, Error>) -> Void)
```

#### API Configuration

**Base URL:**
```
https://dummyjson.com
```

**Endpoint:**
```
/users
```

**Full URL:**
```
https://dummyjson.com/users
```

**Response JSON:**
```
{
    "users": [
        {
            "id": 1,
            "firstName": "Emily",
            "lastName": "Johnson",
            "maidenName": "Smith",
            "age": 29,
            "gender": "female",
            "email": "emily.johnson@x.dummyjson.com",
            "phone": "+81 965-431-3024",
            "birthDate": "1996-5-30",
            "image": "https://dummyjson.com/icon/emilys/128",
            "eyeColor": "Green",
            "address": {
                "address": "626 Main Street",
                "city": "Phoenix",
                "state": "Mississippi",
                "stateCode": "MS",
                "postalCode": "29112",
                "country": "United States"
            },
            "university": "University of Wisconsin--Madison",
            "company": {
                "department": "Engineering",
                "name": "Dooley, Kozey and Cronin",
                "title": "Sales Manager",
                "country": "United States"
            },
            "role": "admin"
        }
    ]
}
```

The API returns a JSON response containing a list of users with detailed information including firstName, lastName, email, age, gender, and more.

### Repository Pattern

- **MANDATORY:** All network requests must go through Repository classes
- ViewModels should never make direct network calls
- Repositories act as the data source abstraction layer
- ViewModels interact with Repositories, Repositories interact with the Network Layer

Example flow:
```
View Controller -> ViewModel -> Repository -> Network Manager -> URLSession
```

---

## Application Requirements

### Functionality

#### Main Screen (User List)
- Fetch users from the provided endpoint
- Display users in a list/table view
- Handle loading states
- Handle error states

**Cell Design:**

Each table view cell must display:
- **Full Name** (firstName + lastName)
- **Email Address** (displayed below the full name)

#### Detail Screen
- Navigate to detail screen when a user is tapped
- Proper data passing between screens

**Information to Display:**

The detail screen must show the following user information:
- **First Name**
- **Last Name**
- **Age**
- **Gender**
- **Email Address**

---

## Evaluation Criteria

### Architecture
- Proper MVVM separation of concerns
- Correct protocol-oriented design
- Appropriate use of Delegate pattern
- Repository pattern implementation

### Code Quality
- Clean, readable code
- Proper naming conventions
- Error handling
- Memory management (avoid retain cycles)

### Functionality
- Working user list
- Working detail screen
- Proper data flow
- UI responsiveness

### Technical Implementation
- Generic network layer
- URLSession usage
- Decodable implementation
- Navigation implementation

---

## Success Tips

- Start with the architecture setup (protocols, delegates)
- Build the network layer first
- Implement the Repository pattern before ViewModels
- Create a simple, working version before adding polish
- Test your data flow as you build
- Manage your time wisely - aim for a working app in 90 minutes

---

## Prohibited Practices

❌ Storyboards or Interface Builder  
❌ SwiftUI (unless explicitly requested)  
❌ Completion handlers for ViewModel-to-View communication  
❌ Direct network calls from ViewModels  
❌ Code comments for explanations  
❌ Multiple example variations  

## Good Luck!

Remember: We're looking for clean architecture, proper patterns, and working functionality. It's better to have a simple, well-structured app than a complex, poorly organized one.
