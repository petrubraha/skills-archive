# Django Testing

## Proper Isolation (Mocks, Patches, and Fake Databases)

Using Python's `unittest.mock` and `unittest.TestCase` to fully mock database models and avoid the database entirely. For example, testing the `message_feed` service in the `trails` app without hitting the database:

```py
import unittest
from unittest.mock import patch, MagicMock
from trails.services import message_feed

class MessageFeedTests(unittest.TestCase):
    def setUp(self):
        # Global mock for a WebSocket broadcast service.
        self.patcher = patch("trails.services.message_feed.broadcast_ws_message")
        self.mock_broadcast = self.patcher.start()
        self.addCleanup(self.patcher.stop)

        # Mocking a database record for a User.
        self.fake_user = MagicMock()
        self.fake_user.id = 1
        self.fake_user.email = "test@varful.ro"

    @patch("trails.services.message_feed.Message")
    def test_send_and_broadcast_user_message(self, mock_message_model):
        mock_created_msg = MagicMock()
        mock_message_model.objects.create.return_value = mock_created_msg

        # Mocking empty validation.
        with patch("trails.services.message_feed.check_message_not_empty", return_value=(True, "", 200)):
            result = message_feed.send_and_broadcast_user_message(
                sender=self.fake_user,
                recipient=self.fake_user,
                raw_content="Hello",
                image_file=None
            )

        self.assertTrue(result[1])
        mock_message_model.objects.create.assert_called_once()
        self.mock_broadcast.assert_called_once_with(mock_created_msg, is_group=False)
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
python manage.py test trails.tests.services.test_message_feed
```

_Note: If the virtual environment is not activated, prefix `python` with the path to the virtual environment's executable (e.g., `.\.venv\Scripts\python.exe` on Windows or `./.venv/bin/python` on Linux)._

## Coverage Commands

Run the tests with coverage gathering, then generate the report for the specific file you are testing.

**Windows / Linux / macOS (Activated Virtual Environment):**

```bash
# 1. Run tests with coverage gathering for a specific test file.
coverage run manage.py test trails.tests.services.test_message_feed

# 2. Generate and print the coverage report to the terminal for the specific source file.
coverage report -m trails/services/message_feed.py
```
