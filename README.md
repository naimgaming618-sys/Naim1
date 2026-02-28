pkg update -y
pkg install git python -y

# Remove old installation if exists
rm -rf $HOME/.ariyan
rm -f $PREFIX/bin/ariyan

# Clone fresh copy
git clone https://github.com/Ariyan20267/Ariyan_bot.git $HOME/.ariyan

# Install requirements
pip install --upgrade pip
pip install -r $HOME/.ariyan/requirements.txt

# Create permanent command
cat << 'EOF' > $PREFIX/bin/ariyan
#!/data/data/com.termux/files/usr/bin/bash
if [ ! -d "$HOME/.ariyan" ]; then
    git clone https://github.com/Ariyan20267/Ariyan_bot.git $HOME/.ariyan
fi

cd $HOME/.ariyan
git pull > /dev/null 2>&1

if [ -f "requirements.txt" ]; then
    pip install -r requirements.txt > /dev/null 2>&1
fi

python ARIYAN.py
EOF

chmod +x $PREFIX/bin/ariyan
