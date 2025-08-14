# Administrator Commands Documentation

This document provides a comprehensive list of all commands available to administrators in the Telegram bot.

## 🆕 New Features

### Interactive Settings Panel
The `/settings` command now provides an interactive panel with buttons for easy management of chat settings.

**Features:**
- **Button Interface:** Toggle settings with one click
- **Real-time Updates:** Settings are saved immediately to database
- **Visual Status:** Clear indicators showing current state (✅/❌)
- **Refresh Option:** Update display without re-running command

### Code Access Management
New system for controlling code message permissions in specific topics.

**Features:**
- **Topic-based Access:** Allow code messages only in specific topics
- **Flexible Control:** Enable/disable code access per topic
- **Database Storage:** All settings saved persistently
- **Admin-only Management:** Only administrators can configure

### Enhanced Link Filtering
Improved link filtering system with strict whitelist enforcement.

**Features:**
- **Whitelist-only Mode:** Only links from whitelist are allowed
- **Automatic Blocking:** Non-whitelisted links are automatically blocked
- **Detailed Reporting:** Shows which specific links were blocked
- **Database Integration:** Whitelist stored in database

## Moderation Commands

### Message Moderation

#### `/settings` - Manage Chat Settings
Controls general chat settings with an interactive button interface for easy management.

**Interactive Panel:**
- `/settings` - Display interactive settings panel with buttons
- **Cyrillic:** Toggle Cyrillic text allowance
- **Links:** Toggle link filtering (whitelist-only mode)
- **Forwards:** Toggle forwarded message allowance
- **Code:** Toggle code message processing
- **Admin Notify:** Toggle detailed admin notifications
- **Whitelist:** Quick access to whitelist management
- **Refresh:** Update settings display

**Legacy Commands (still supported):**
- `/settings cyrillic allow/block` - Allow or block Cyrillic text
- `/settings links allow/block` - Allow or block links in messages
- `/settings forwards allow/block` - Allow or block forwarded messages
- `/settings code ignore/process` - Ignore or process messages containing code
- `/settings adminnotify enable/disable` - Enable or disable detailed admin notifications

**Features:**
- **One-click Toggle:** Change settings instantly with buttons
- **Visual Feedback:** Clear status indicators (✅/❌)
- **Real-time Save:** Settings saved to database immediately
- **Admin-only Access:** Only administrators can modify settings

#### `/adminnotify` - Toggle Admin Notifications
Quickly toggle whether to send detailed notifications to admins about rule violations.

**Usage:**
- `/adminnotify` - Toggle the admin notification setting on/off

#### `/codeignore` - Toggle Code Ignoring
Quickly toggle whether to ignore messages containing code snippets (PHP, Python, JavaScript, etc.).

**Usage:**
- `/codeignore` - Toggle the code ignoring setting on/off

#### `/testcode` - Test Code Detection
Test if a message would be detected as code and ignored by the bot.

**Usage:**
- Reply to any message with `/testcode` to check if it would be detected as code

#### `/codeaccess` - Manage Code Access Permissions
Control which topics allow code messages and manage code access settings.

**Usage:**
- `/codeaccess` - Display current code access settings
- `/codeaccess enable <topic_id>` - Enable code access for specific topic
- `/codeaccess disable` - Disable code access for all topics
- `/codeaccess topic <topic_id>` - Set topic ID for code access without enabling

**Features:**
- **Topic-specific Access:** Code messages allowed only in specified topics
- **Flexible Control:** Enable/disable access independently of topic setting
- **Database Storage:** Settings saved persistently
- **Admin-only:** Only administrators can manage code access

#### `/whitelist` - Manage Whitelisted Links
Manage a list of domain patterns that are allowed even when links are generally blocked.

**Usage:**
- `/whitelist` - Display current whitelisted domains
- `/whitelist add example\.com` - Add a domain pattern to the whitelist
- `/whitelist remove example\.com` - Remove a domain pattern from the whitelist
- `/whitelist clear` - Clear all whitelisted domains

#### `/warnings` - Manage User Warnings
View and manage warnings that have been issued to users.

**Usage:**
- `/warnings` - Show all users with warnings in the chat
- `/warnings [user_id]` - Show warnings for a specific user
- Use the "Remove warning" button to remove a warning (admin only)
- Use the "Clear all warnings" button to clear all warnings for a user (admin only)

### Content Filtering

#### `/censure_settings` - Manage Obscenity Filter
Controls the obscenity filter settings for the chat.

**Usage:**
- `/censure_settings` - Display current settings
- `/censure_settings enable/disable` - Enable or disable the obscenity filter
- `/censure_settings language ru/en/both` - Set which languages to filter (Russian, English, or both)

#### `/banned_content` - Manage Banned Words and Emojis
Controls the list of banned words and emojis in the chat.

**Usage:**
- `/banned_content` - Display current banned content
- `/banned_content add word1, word2, ...` - Add words to the banned list
- `/banned_content add_emoji 😀, 😂, ...` - Add emojis to the banned list
- `/banned_content remove word1, word2, ...` - Remove words from the banned list
- `/banned_content remove_emoji 😀, 😂, ...` - Remove emojis from the banned list
- `/banned_content clear` - Clear all banned content

### Reporting System

#### `/report` - Report Messages
While this command is available to all users, admins receive these reports.

**Usage:**
- Reply to a message with `/report` to report it to administrators

### Ban Management

#### `/banid` - Check or Ban User IDs
Check if a user ID is banned or ban a user ID.

**Usage:**
- `/banid [user_id]` - Check if a user ID is banned

### Code Access Management

Manage code message permissions for different topics.

**Usage:**
- `/codeaccess` - Show current code access settings
- `/codeaccess enable` - Enable code access globally
- `/codeaccess disable` - Disable code access globally
- `/codeaccess add <topic_id>` - Add topic to access list (disabled by default)
- `/codeaccess remove <topic_id>` - Remove topic from access list
- `/codeaccess enable_topic <topic_id>` - Enable specific topic for code access
- `/codeaccess disable_topic <topic_id>` - Disable specific topic for code access
- `/codeaccess list` - Show all configured topics with their status

**Example:**
```
/codeaccess add 123456789
/codeaccess enable_topic 123456789
/codeaccess add 987654321
/codeaccess list
```

## System Behavior

### Warning System
- When a user violates chat rules (using banned words, posting links when not allowed, etc.), they receive a warning
- After 5 warnings, the user is automatically banned from the chat
- Only administrators can remove warnings using the inline buttons on warning messages

### Content Filtering
- Messages containing banned words or emojis are automatically deleted
- Messages in languages other than those allowed (Russian and English by default) are deleted
- Messages containing obscene language are deleted based on the censure settings
- **Code Messages:** 
  - Can be ignored globally based on settings
  - Can be allowed only in specific topics when code access is enabled
  - Support for multiple topics with individual access control
  - Each topic can be enabled/disabled independently
  - Blocked in all other topics when topic-specific access is configured
- **Link Filtering:**
  - **Whitelist-only Mode:** Only links from whitelist are allowed
  - **Automatic Blocking:** Non-whitelisted links are automatically blocked
  - **Detailed Reporting:** Shows which specific links were blocked

### Admin Privileges
- Administrators are exempt from content filtering and warning systems
- Only administrators can change chat settings and manage banned content
- Administrators receive reports submitted by users
- Administrators receive detailed notifications about rule violations with options to restore messages or remove warnings
- Notifications include clickable user IDs, violation details, and message previews

## Database Integration

### Settings Persistence
- **MySQL Database:** All settings stored in MySQL database
- **Chat-specific Settings:** Each chat has independent settings
- **Automatic Save:** Settings saved immediately when changed
- **Persistent Storage:** Settings maintained between bot restarts

### New Database Fields
- **`allow_code_access`:** Controls code message permissions
- **`topic_access_list`:** Stores list of topics with access permissions (JSON array of objects with topic_id and enabled status)
- **Enhanced Settings:** All existing settings with improved storage

## Notes
- Each chat has its own independent settings for banned content, censure settings, and general settings
- Settings are persistent and will be maintained even if the bot is restarted
- Some features may require the bot to have appropriate permissions in the chat (delete messages, ban users, etc.)
- **New:** Interactive settings panel provides easier management than command-line options
- **New:** Code access can be restricted to specific topics for better organization
- **New:** Link filtering now uses strict whitelist-only mode by default 
