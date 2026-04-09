# Example Output: Login Feature

## Input Provided

> **User Story:** As a registered user, I want to log in with my email and password so I can access my account. The system should lock the account after 5 failed attempts. Password is required. Email must be valid format. A "Remember Me" checkbox is available. Admin users see a different dashboard than standard users after login.

---

## Generated Test Cases

| Test ID | Test Case Name | Creation Date | Designer | Equivalence | Priority | Purpose | Pre-Conditions | Test Data | Category | Step No. | Description | Expected Result |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| TC-001 | Login with Valid Email and Password | 09-Apr-2025 | [Your Name] | Valid Input | High | Validates that a registered user can log in successfully with correct credentials | 1. The application is running and accessible. 2. A registered user account exists with known credentials. 3. The user is on the Login page. | Role: 'Standard User', Email: 'john.doe@example.com', Password: 'Password@123', Remember Me: unchecked | Primary Workflow | 1 | Navigate to the Login page at Home > Login. | The Login page loads with an "Email" field, a "Password" field, a "Remember Me" checkbox, and a "Login" button visible. |
| | | | | | | | | | | 2 | Click the "Email" field and type 'john.doe@example.com'. | The email address 'john.doe@example.com' appears in the "Email" field. |
| | | | | | | | | | | 3 | Click the "Password" field and type 'Password@123'. | The "Password" field shows masked characters (dots or asterisks) for each character typed. |
| | | | | | | | | | | 4 | Click the "Login" button. | The system authenticates the user and redirects to the Standard User dashboard at Home > Dashboard. |
| TC-002 | Login Redirects Admin to Admin Dashboard | 09-Apr-2025 | [Your Name] | Valid Input - Role Variant | High | Validates that Admin users land on the Admin dashboard, not the standard one | 1. The application is running. 2. An Admin account exists with known credentials. 3. The user is on the Login page. | Role: 'Admin', Email: 'admin@example.com', Password: 'AdminPass@1' | Role-Based Access | 1 | Navigate to the Login page at Home > Login. | The Login page loads. |
| | | | | | | | | | | 2 | Enter 'admin@example.com' in the "Email" field and 'AdminPass@1' in the "Password" field. | Credentials are entered. |
| | | | | | | | | | | 3 | Click the "Login" button. | The system redirects to the Admin dashboard at Home > Admin Dashboard. The standard user dashboard is not shown. |
| TC-003 | Login Blocked with Incorrect Password | 09-Apr-2025 | [Your Name] | Invalid Input | High | Validates that login fails and shows an error when password is wrong | 1. A registered user account exists. 2. The user is on the Login page. | Role: 'Standard User', Email: 'john.doe@example.com', Password: 'WrongPass99' | Error Handling | 1 | Navigate to Home > Login. | The Login page loads. |
| | | | | | | | | | | 2 | Enter 'john.doe@example.com' in the "Email" field and 'WrongPass99' in the "Password" field. | Credentials are entered. |
| | | | | | | | | | | 3 | Click the "Login" button. | The system does not log the user in. An error message appears: 'Invalid email or password.' The user remains on the Login page. |
| TC-004 | Account Locks After 5 Failed Login Attempts | 09-Apr-2025 | [Your Name] | Boundary Value | High | Validates the account lockout rule triggers at exactly 5 failed attempts | 1. A registered, unlocked account exists. 2. The user is on the Login page. | Role: 'Standard User', Email: 'lock.test@example.com', Password (wrong): 'BadPass001' (used 5 times) | Edge & Boundary | 1 | Navigate to Home > Login. Enter 'lock.test@example.com' and 'BadPass001'. Click "Login". Repeat this step 4 more times (5 total failed attempts). | After the 5th failed attempt, an error message appears: 'Your account has been locked due to too many failed attempts. Please contact support.' |
| | | | | | | | | | | 2 | Enter 'lock.test@example.com' and the correct password in the Login form. Click "Login". | The system blocks login and displays: 'Your account has been locked.' The user is not authenticated. |
| TC-005 | Login Blocked When Email Field is Empty | 09-Apr-2025 | [Your Name] | Invalid Input - Missing Required | High | Validates that the system blocks submission when email is empty | 1. The user is on the Login page. | Role: 'Standard User', Email: '' (empty), Password: 'Password@123' | Error Handling | 1 | Navigate to Home > Login. Leave the "Email" field empty. Enter 'Password@123' in the "Password" field. Click "Login". | The system blocks submission and displays an inline error below the "Email" field: 'Email address is required.' |
| TC-006 | Login Blocked When Password Field is Empty | 09-Apr-2025 | [Your Name] | Invalid Input - Missing Required | High | Validates that the system blocks submission when password is empty | 1. The user is on the Login page. | Role: 'Standard User', Email: 'john.doe@example.com', Password: '' (empty) | Error Handling | 1 | Navigate to Home > Login. Enter 'john.doe@example.com' in the "Email" field. Leave the "Password" field empty. Click "Login". | The system blocks submission and displays an inline error below the "Password" field: 'Password is required.' |
| TC-007 | Login Blocked with Malformed Email Format | 09-Apr-2025 | [Your Name] | Invalid Input - Format | Medium | Validates that the system rejects email addresses that do not follow valid format rules | 1. The user is on the Login page. | Role: 'Standard User', Email: 'notanemail' (no @ or domain), Password: 'Password@123' | Error Handling | 1 | Navigate to Home > Login. Enter 'notanemail' in the "Email" field. Enter 'Password@123' in the "Password" field. Click "Login". | The system blocks submission and displays: 'Please enter a valid email address.' |
| TC-008 | Remember Me Checkbox Persists Session | 09-Apr-2025 | [Your Name] | Alternate Flow | Medium | Validates that checking Remember Me keeps the user logged in after browser is closed and reopened | 1. A registered user account exists. 2. The user is on the Login page. | Role: 'Standard User', Email: 'john.doe@example.com', Password: 'Password@123', Remember Me: checked | Alternate Flow | 1 | Navigate to Home > Login. Enter valid credentials. Check the "Remember Me" checkbox. Click "Login". | The user is logged in and redirected to the dashboard. |
| | | | | | | | | | | 2 | Close the browser completely and reopen it. Navigate back to the application URL. | The user is automatically logged in and lands on the dashboard without being prompted for credentials. |

---

## Test Case Summary

**Total Test Cases Generated:** 8

**Breakdown by Category:**
- Primary Workflow: 1
- Alternate Flow: 1
- Error Handling: 3
- Edge & Boundary: 1
- Role-Based Access: 1
- (Note: TC-001 also serves as the baseline for role comparison in TC-002)

**Requirements / User Stories Covered:**
- Login User Story: Covered by TC-001 through TC-008

**Coverage Confirmation:**
All primary, alternate, error, edge, and role-based paths have been tested.

**Assumptions Made:**
- The exact text of error messages ('Invalid email or password.', 'Email address is required.' etc.) was not specified in the user story. Text used in Expected Results is assumed. Replace with exact copy from UI specs before test execution.
- "Remember Me" persistence mechanism (cookie vs. session token) was not defined. TC-008 tests observable behavior only (user stays logged in after browser close).
- Account unlock mechanism (admin unlock vs. time-based) was not specified. TC-004 verifies lockout occurs but does not test the unlock flow.
