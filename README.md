# OpenCode Behavior Adjustment System (BAS) Plugin

This plugin enhances technical collaboration by injecting contextual behavioral reminders based on conversation content.

## Features

- **Contextual Awareness**: Detects conversation topics (Code Review, Architecture, Debugging, etc.) and applies relevant behavioral templates.
- **Adaptive Model Parameters**: Adjusts model temperature and other parameters based on the detected context.
- **Template Deduplication**: Resolves multiple matching contexts using priority-based deduplication.
- **Configurable Injection Rates**: Controls how often reminders are injected.
- **Detailed Logging**: Optional logging of injection events for analysis.

## Configuration

The plugin loads configuration from:

1. `~/.config/opencode/behavior-config.json` (User-level)
2. `.opencode/behavior-config.json` (Project-level)

Project-level configuration takes precedence.

### Example `behavior-config.json`

```json
{
  "enabled": true,           // Global toggle for the plugin
  "adaptiveMode": true,      // If true, detects context from message text; else uses 'default'
  "logging": true,           // Enables logging of injection events to ~/.config/opencode/behavior-adjustment.log
  "contexts": {
    "default": {             // Fallback context
      "template": "balanced",// Template name to use
      "injectionRate": 0.4,  // Probability (0.0 to 1.0) of injecting the reminder
      "priority": 1,         // Priority for deduplication when multiple contexts match
      "temperature": 0.3     // Optional: model temperature adjustment for this context
    }
  },
  "templates": {
    "balanced": {
      "type": "behavior",    // Arbitrary type string (used for priority-based deduplication)
      "prompt": [            // The actual content to inject (string or array of strings)
        "<system-reminder>",
        "Maintain technical peer stance. Evaluate before responding.",
        "</system-reminder>"
      ]
    }
  }
}
```

## Installation

Add the plugin to your `opencode.json`:

```json
{
  "plugin": ["@fedaykindev/opencode-bas-plugin"]
}
```

## License

MIT
