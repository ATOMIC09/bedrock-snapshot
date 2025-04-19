# Bedrock World Snapshot

<p>
  <img alt="GitHub Release" src="https://img.shields.io/github/v/release/ATOMIC09/bedrock-snapshot">
  <img alt="GitHub License" src="https://img.shields.io/github/license/ATOMIC09/bedrock-snapshot">
  <a href="https://github.com/ATOMIC09/chunky-timelapse/tags">
      <img alt="Download" src="https://img.shields.io/github/downloads/ATOMIC09/chunky-timelapse/total" />
  </a>
</p>

A utility script for creating snapshots of Minecraft Bedrock worlds, converting them to Java format, rendering beautiful images using Chunky, and sending them to Discord.

![script_thumbnail](https://github.com/user-attachments/assets/63997db8-709b-48ed-ae8e-966a8e94b46e)

## Features

- Convert Minecraft Bedrock worlds to Java format
- Automatically render worlds using Chunky
- Extract world information (such as in-game day)
- Send notifications and rendered images via Discord webhooks
- Automatic download of dependencies (chunker-cli and Chunky)
- Flexible configuration options

## Requirements

- Bash shell environment (Linux, macOS, or Windows with WSL/Git Bash)
- Java 17 or higher
- Internet connection for automatic dependency downloads (or manual placement of dependencies)
- Optional: wget or curl (for automatic dependency downloads)

## Installation

1. Clone this repository:
   ```
   git clone https://github.com/ATOMIC09/bedrock-snapshot.git
   cd bedrock-snapshot
   ```

2. Make the script executable:
   ```
   chmod +x bedrock_world_snapshot.sh
   ```

3. Dependencies:
   - The script will **automatically download** the required dependencies:
     - [chunker-cli-1.7.0.jar](https://github.com/HiveGamesOSS/Chunker/releases/download/1.7.0/chunker-cli-1.7.0.jar) for Bedrock to Java conversion
     - [Chunky Launcher](https://chunky.llbit.se/) for rendering
   - If you prefer to download manually, place them in the same directory as the script

## Setup

Before running the script, you'll need:

1. A Minecraft Bedrock or Java world to convert
2. A pre-configured Chunky scene for rendering. You can create a scene using the Chunky GUI then copy the scene folder to the `.chunky/scenes` directory.

### Creating a Chunky Scene

1. Install and run Chunky
2. Create a new scene and configure it with your desired camera position, FOV, etc.
3. Remember the scene name for use with this script

## Usage

Basic usage:

```bash
./bedrock_world_snapshot.sh
```

This will use default settings. For more options:

```bash
./bedrock_world_snapshot.sh -h
```

### Common Options

- `-i INPUT_DIR` - Directory containing Bedrock worlds
- `-o OUTPUT_DIR` - Output directory for Java worlds
- `-w WORLD_NAME` - Specific world folder name inside INPUT_DIR
- `-n SCENE_NAME` - Scene name for Chunky render *(required)*
- `-u WEBHOOK_URL` - Discord webhook URL for notifications
- `-r` - Take a snapshot after conversion (default)
- `-b` - Skip Bedrock to Java conversion (use existing Java world)

### Example: Convert Bedrock to Java and Render then send to Discord

```bash
./bedrock_world_snapshot.sh \
  -i "$HOME/bedrock-snapshot/bedrock_worlds" \
  -n "my_scene" \
  -u "https://discord.com/api/webhooks/your-webhook-url" \

```

If you got "Error: Scene directory `.chunky/scenes/scene1` not found!", you have to copy your scene folder to the `.chunky/scenes` directory. 

Then, you can run the script again with the `-b` option to skip the conversion step:


### Example: Render existing Java world and send to Discord

```bash
./bedrock_world_snapshot.sh \
  -b \
  -o "$HOME/bedrock-snapshot/java_worlds" \
  -n "my_scene" \
  -u "https://discord.com/api/webhooks/your-webhook-url" \
```

## Automation

You can set up a cron job to take regular snapshots:

```bash
# Edit crontab
crontab -e

# Add line to run daily at midnight
0 0 * * * cd /path/to/bedrock-snapshot && ./bedrock_world_snapshot.sh
```

## Known Issues

- The script requires proper configuration of Chunky scenes beforehand
- Large worlds may take significant time to convert and render

## License

See the [LICENSE](LICENSE) file for details.
