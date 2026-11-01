# Django Testing

## Proper Isolation (Mocks, Patches, and Fake Databases)

Using Python's `unittest.mock` and `unittest.TestCase` to fully mock database models and avoid the database entirely. For example, testing the `order_service` module in the `orders` app without hitting the database:

```py
import unittest
from unittest.mock import MagicMock, patch

from ...services import order_service

class PlaceOrderTests(unittest.TestCase):
    def setUp(self):
        # Global mock for the kitchen display notification.
        self.patcher = patch("orders.services.order_service.notify_kitchen")
        self.mock_notify_kitchen = self.patcher.start()
        self.addCleanup(self.patcher.stop)

        # Mocking a database record for a customer.
        self.fake_customer = MagicMock()
        self.fake_customer.id = 1
        self.fake_customer.email = "customer@example.com"

    @patch("orders.services.order_service.Order")
    def test_place_order_notifies_kitchen(self, mock_order_model):
        mock_created_order = MagicMock()
        mock_order_model.objects.create.return_value = mock_created_order

        # Mocking the delivery area check.
        with patch("orders.services.order_service.is_in_delivery_area", return_value=True):
            result = order_service.place_order(
                customer=self.fake_customer,
                pizza_ids=[3, 7],
                delivery_address="1 Main Street",
            )

        self.assertEqual(result, mock_created_order)
        mock_order_model.objects.create.assert_called_once()
        self.mock_notify_kitchen.assert_called_once_with(mock_created_order)
```

## Test Scope

Changes to these reach far, so run the full suite (`python manage.py test`) after editing them:

- `models.py` or any migration.
- `settings.py` (or a split settings package).
- Middleware.
- `signals.py` and signal receivers.
- Barrel modules that re-export across the app, such as a `models/__init__.py` or `utils/__init__.py`.
- Base templates that others `{% extends %}`.

## Dependencies

To check if `coverage` is installed, you can attempt to run it or check the installed packages. If missing, install it within the active virtual environment depending on your operating system:

**Windows (PowerShell):**

```powershell
.\.venv\Scripts\python.exe -m pip install coverage
```

**Linux / macOS:**

```bash
./.venv/bin/python -m pip install coverage
```

## Test Commands

Always use the standard Django test runner to run tests. Provide the specific module path to speed up execution.

**Windows / Linux / macOS (Activated Virtual Environment):**

```bash
python manage.py test orders.tests.services.test_order_service
```

_Note: If the virtual environment is not activated, prefix `python` with the path to the virtual environment's executable (e.g., `.\.venv\Scripts\python.exe` on Windows or `./.venv/bin/python` on Linux)._

## Coverage Commands

Run the tests with coverage gathering, then generate the report for the specific file you are testing.

**Windows / Linux / macOS (Activated Virtual Environment):**

```bash
# 1. Run tests with coverage gathering for a specific test file.
coverage run manage.py test orders.tests.services.test_order_service

# 2. Generate and print the coverage report to the terminal for the specific source file.
coverage report -m orders/services/order_service.py
```
