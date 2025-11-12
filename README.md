name: Free VPS

on:
  workflow_dispatch:  # Manual start
  schedule:
    - cron: '0 */6 * * *'  # Optional: auto run every 6 hours

jobs:
  build:
    runs-on: ubuntu-latest
    timeout-minutes: 360  # 6 hours max

    steps:
      - name: Start VPS
        run: |
          echo "Updating packages..."
          sudo apt update -y && sudo apt upgrade -y
          echo "Installing basic tools..."
          sudo apt install -y wget curl unzip git

          echo "System Info:"
          uname -a
          lscpu
          free -h
          df -h

          # Example: Install Node.js
          echo "Installing Node.js..."
          curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
          sudo apt install -y nodejs

          node -v
          npm -v

          echo "Your temporary VPS is ready!"
          echo "You can use Cloudflared or Ngrok for SSH access"# Hosting-Actions → New workflow → set up a workflow yourself
