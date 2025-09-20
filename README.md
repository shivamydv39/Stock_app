## Project Description

This project is a responsive **stock trading dashboard** developed using the **Flutter framework**

### Objectives

* Develop a pixel-perfect replica of a trading dashboard interface.
* Implement a responsive design suitable for multiple device categories.
* Provide functional filtering and search mechanisms.
* Apply software engineering best practices with clean, maintainable code.
* Demonstrate proficiency in Flutter and Dart programming.

---

## Features Implemented

### Advanced Filtering System

Implemented dynamic filtering for stock orders with support for both stock symbol filtering and keyword search.

```dart
List<StockOrder> get filteredOrders {
  List<StockOrder> filtered = allOrders;
  
  if (activeStockFilters.isNotEmpty) {
    filtered = filtered.where((order) =>
      activeStockFilters.contains(order.stockSymbol)
    ).toList();
  }
  
  if (searchQuery.isNotEmpty) {
    filtered = filtered.where((order) =>
      order.stockSymbol.toLowerCase().contains(searchQuery.toLowerCase()) ||
      order.clientCode.toLowerCase().contains(searchQuery.toLowerCase())
    ).toList();
  }
  
  return filtered;
}
```

### Responsive Design

* Breakpoint-based layouts: Desktop (>900px), Tablet (600–900px), Mobile (<600px).
* Adaptive table structures: Collapsed stacked rows on mobile and expanded tables on desktop.
* Dynamic headers: Column headers adjust according to available space.
* Collapsible navigation: Navigation elements adjust to smaller screens.

### Custom UI Components

* Market data app bar
* Filter chips with remove functionality
* Real-time search bar
* Responsive data tables with custom rendering

---

## Technical Architecture

**Design Pattern:** StatefulWidget-based state management

**Screen Structure:**

```
TradingOrdersScreen (StatefulWidget)
├── State Management Layer
│   ├── activeStockFilters (List<String>)
│   ├── searchQuery (String)
│   └── allOrders (List<StockOrder>)
├── Business Logic Layer
│   ├── filteredOrders (Computed Property)
│   ├── removeStockFilter() (Method)
│   └── updateSearchQuery() (Method)
└── Presentation Layer
    ├── UI Components
    └── Responsive Layouts
```

**Data Model Example:**

```dart
class StockOrder {
  final String timestamp;
  final String clientCode;
  final String stockSymbol;
  final String orderType;      // Buy/Sell
  final String productType;    // CNC/NRML/INTRADAY
  final String executedQuantity;
  final String totalQuantity;
  final String orderPrice;
  final bool hasInfoIcon;
}
```

---



## Responsive Design Strategy

### Breakpoint Handling

```dart
Widget _createTableHeaderSection() {
  return LayoutBuilder(
    builder: (context, constraints) {
      if (constraints.maxWidth < 900) {
        return Column(
          children: [
            _createHeaderRow(['Time', 'Client', 'Stock Symbol']),
            _createHeaderRow(['Side', 'Product', 'Quantity', 'Price', 'Actions']),
          ],
        );
      } else {
        return Row(
          children: [
            _createHeaderColumn('Time', flex: 1),
            _createHeaderColumn('Client', flex: 1),
            // Additional columns...
          ],
        );
      }
    },
  );
}
```

**Techniques Used:**

* LayoutBuilder for conditional layouts
* MediaQuery for device-specific adjustments
* Flexible & Expanded widgets for proportional space usage
* Container constraints to maintain uniform spacing


## Installation & Setup

### Requirements

* Flutter SDK 3.0+
* Dart 3.0+
* Android Studio or VS Code
* Git

### Steps

```bash
git clone https://github.com/your-username/stock-trading-dashboard.git
cd stock-trading-dashboard
flutter pub get
flutter run
```

### Build Commands

* Debug build: `flutter run --debug`
* Release build (Android): `flutter build apk --release`
* Release build (Web): `flutter build web --release`
* Release build (Windows): `flutter build windows --release`

---

## Testing & Validation

### Testing Types

* Unit tests for business logic
* Widget tests for UI behavior
* Integration tests for full workflows
* Cross-device responsive validation

**Example Test Case:**

```dart
testWidgets('Filter functionality test', (WidgetTester tester) async {
  await tester.pumpWidget(StockTradingApp());
  
  expect(find.text('RELIANCE'), findsOneWidget);
  expect(find.text('ASIANPAINT'), findsOneWidget);
  
  await tester.tap(find.byIcon(Icons.close_rounded).first);
  await tester.pump();
  
  expect(find.text('RELIANCE'), findsNothing);
});
```

**Performance Optimizations:**

* `ListView.builder` for large datasets
* Use of `const` constructors
* Computed properties for derived states
* Optimized `setState` usage to minimize rebuilds

---

## Challenges & Solutions

1. **Responsive Table Design**

   * Challenge: Maintaining usability across devices.
   * Solution: Used `LayoutBuilder` with condition-based rendering.

2. **Real-time Filtering Performance**

   * Challenge: Filtering large datasets caused lag.
   * Solution: Introduced computed properties and efficient filtering logic.


---

## Future Enhancements

**Phase 1:**

* WebSocket integration for live data
* Multi-column sorting
* Export options (CSV/PDF)
* Dark mode support

**Phase 2:**

* REST API integration
* User authentication
* Real-time notifications
* Database persistence

**Phase 3:**

* Interactive charts
* Portfolio metrics
* Data visualization dashboards

---

## Learning Outcomes

### Technical Skills

* Advanced Flutter and Dart concepts
* Responsive cross-platform design
* Clean architecture and code organization
* UI/UX design principles
* Performance optimization

### Software Engineering Practices

* Applied SOLID principles
* Used Git effectively for version control
* Documented code and project setup thoroughly
* Applied iterative development and peer feedback

### Problem-Solving Approach

* Analyzed requirements into smaller components
* Researched Flutter documentation and community practices
* Developed features iteratively and tested continuously
* Performed self-review and improvements during development

-
Would you like me to also prepare this in a **concise, formal report format (8–10 pages, with abstract, introduction, conclusion)** so that it looks like a **final-year project submission document**?
