# Administrator Commands Documentation

This document provides a comprehensive list of all commands available to administrators in the Telegram bot.

## Moderation Commands

### Message Moderation

#### `/settings` - Manage Chat Settings
Controls general chat settings such as allowing/blocking Cyrillic text, links, and forwarded messages.

**Usage:**
- `/settings` - Display current settings
- `/settings cyrillic allow/block` - Allow or block Cyrillic text
- `/settings links allow/block` - Allow or block links in messages
- `/settings forwards allow/block` - Allow or block forwarded messages
- `/settings code ignore/process` - Ignore or process messages containing code

#### `/codeignore` - Toggle Code Ignoring
Quickly toggle whether to ignore messages containing code snippets (PHP, Python, JavaScript, etc.).

**Usage:**
- `/codeignore` - Toggle the code ignoring setting on/off

#### `/testcode` - Test Code Detection
Test if a message would be detected as code and ignored by the bot.

**Usage:**
- Reply to any message with `/testcode` to check if it would be detected as code

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

## System Behavior

### Warning System
- When a user violates chat rules (using banned words, posting links when not allowed, etc.), they receive a warning
- After 5 warnings, the user is automatically banned from the chat
- Only administrators can remove warnings using the inline buttons on warning messages

### Content Filtering
- Messages containing banned words or emojis are automatically deleted
- Messages in languages other than those allowed (Russian and English by default) are deleted
- Messages containing obscene language are deleted based on the censure settings
- Messages containing code snippets (PHP, Python, JavaScript, etc.) can be ignored based on settings
- Links are blocked unless they match patterns in the whitelist

### Admin Privileges
- Administrators are exempt from content filtering and warning systems
- Only administrators can change chat settings and manage banned content
- Administrators receive reports submitted by users

## Notes
- Each chat has its own independent settings for banned content, censure settings, and general settings
- Settings are persistent and will be maintained even if the bot is restarted
- Some features may require the bot to have appropriate permissions in the chat (delete messages, ban users, etc.) 
