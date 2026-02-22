Here's an enhanced version of your conference plan integrating key techniques from Martin Fowler's Refactoring and Michael Feathers' Working Effectively with Legacy Code, with tactical implementations for each segment:

Part 2: Refactor vs. Rewrite – Enhanced Decision Framework
Feathers' Legacy Code Dilemma:

"To change code safely, you need tests. To add tests, you often need to changecode.

Decision Triggers:

Fowler's Code Smells ():

Divergent Change (multiple modifications for one feature)

Shotgun Surgery (one change requires many edits)

Feature Envy (methods excessively access another class' data)

Use these smells to quantify technical debt during evaluation.

Feathers' Seam Identification :

Demonstrate using object seams (polymorphism) and link seams (dependency injection) to isolate legacy components during assessment.

Live Demo:

Use Sprout Method  to add new currency validation alongside legacy code without modifying existing logic:

java
// Legacy method (untouched)  
void processPayment(Amount amount) { /* ... */ }

// New sprout method (tested)  
void validateCurrency(Currency currency) {  
if (!SUPPORTED_CURRENCIES.contains(currency)) {  
throw new InvalidCurrencyException();  
}  
}  
Show Fowler's Extract Method  to modularize a 50-line legacy function into named, testable components.

Part 3: Testing Strategies – Feathers/Fowler Synthesis
Characterization Testing (Feathers) :

Live demo using ApprovalTests to capture legacy system output:

python
def test_legacy_invoice_calculation():  
result = legacy_calculate_invoice(orders)  
verify(result)  # Records current behavior as baseline  
Test-Driven Refactoring (Fowler) :

Identify Fowler's Primitive Obsession smell in a date-handling class.

Apply Replace Primitive with Object:

javascript
// Before  
function calculateDueDate(isoString) { /* ... */ }

// After  
class DueDate {  
constructor(isoString) { /* ... */ }  
calculate() { /* ... */ }  
}  
Dependency Breaking (Feathers) :

Demo Subclass and Override to isolate a database call:

java
public class OrderProcessor {  
// Legacy method with hidden dependency  
protected void saveToDatabase(Order order) { /* ... */ }

// Testable version  
public void process(Order order) {  
validate(order);  
saveToDatabase(order);  
}  
}

// Test subclass  
class TestOrderProcessor extends OrderProcessor {  
@Override  
protected void saveToDatabase(Order order) {  
// No-op for testing  
}  
}  
Part 4: Advanced Refactoring Toolkit
Fowler's Catalog Techniques :

Scenario	Technique	Example
Complex conditionals	Decompose Conditional	Split 10-line if into isEligible() method
Data clusters	Introduce Parameter Object	Replace (lat, lng) with GeoCoordinate class
Tight coupling	Hide Delegate	Encapsulate third-party API calls behind facade
Feathers' Emergency Patterns :

Wrap Method:

ruby
def save_user(user)  
legacy_save(user)  # Original untested method  
NewUserAuditService.log(user)  # Wrapped functionality  
end  
Preservation Techniques:

Parallel Change: Run old/new systems concurrently during rewrite

Feature Flags: Gradually enable refactored components