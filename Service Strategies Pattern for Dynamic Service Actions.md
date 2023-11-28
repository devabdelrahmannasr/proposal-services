# Technical Proposal: Service Strategies Pattern for Dynamic Service Actions

## Objectives

1. **Dynamic Service Types:** Implement a flexible system to accommodate various service types, ensuring extensibility for future additions.

2. **Action-Specific Logic:** Develop distinct logic for each action based on the service type, allowing for specialized processing tailored to the unique requirements of each service.

3. **Code Reusability:** Design a modular system that promotes code reusability, making it easy to maintain and extend the application.

## Proposed Solution

### 1. `ServiceType` Interface

Create a common interface, `ServiceTypeInterface`, that defines the basic structure for service types. Each service type (Sport, Gateway, Entertainment) will implement this interface.

```php
<?php
interface ServiceTypeInterface {
    public function getTypeName(): string;
}
```

### 2. Service Actions Interfaces

Define interfaces for each service action (CheckAvailability, Calculate, Book, GetBookingDetails), ensuring consistency in the implementation of actions across different service types.

```php
interface CheckAvailabilityInterface {
    public function checkAvailability(): bool;
}

interface CalculateInterface {
    public function calculate(): float;
}

interface BookInterface {
    public function book(): bool;
}

interface GetBookingDetailsInterface {
    public function getBookingDetails(): array;
}
```

### 3. Service Type Implementations

For each service type (Sport, Gateway, Entertainment), create classes that implement both the ServiceTypeInterface and the action-specific interfaces.

```php
class SportService implements ServiceTypeInterface, CheckAvailabilityInterface, CalculateInterface, BookInterface, GetBookingDetailsInterface {
    // Implementation for each interface method
}

class GatewayService implements ServiceTypeInterface, CheckAvailabilityInterface, CalculateInterface, BookInterface, GetBookingDetailsInterface {
    // Implementation for each interface method
}

class EntertainmentService implements ServiceTypeInterface, CheckAvailabilityInterface, CalculateInterface, BookInterface, GetBookingDetailsInterface {
    // Implementation for each interface method
}
```

### 4. Service Strategy Context

Develop a service strategy context class that dynamically sets the service type and invokes the appropriate action.

```php
class ServiceStrategyContext {
    private $serviceType;

    public function setServiceType(ServiceTypeInterface $serviceType) {
        $this->serviceType = $serviceType;
    }

    public function executeCheckAvailability() {
        return $this->serviceType->checkAvailability();
    }

    public function executeCalculate() {
        return $this->serviceType->calculate();
    }

    public function executeBook() {
        return $this->serviceType->book();
    }

    public function executeGetServiceDetails() {
        return $this->serviceType->getBookingDetails();
    }

    public function executeGetBookingDetails() {
        return $this->serviceType->getBookingDetails();
    }
}
```

### Usage Example

```php
$sportService = new SportService();
$context = new ServiceStrategyContext();
$context->setServiceType($sportService);

// Example usage
$availability = $context->executeCheckAvailability();
$calculation = $context->executeCalculate();
$booking = $context->executeBook();
$bookingDetails = $context->executeGetBookingDetails();
```
