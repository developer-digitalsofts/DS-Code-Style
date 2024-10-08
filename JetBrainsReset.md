
# Resetting Trial Period for JetBrains Products

In some cases, only these lines will work:

```sh
for product in IntelliJIdea WebStorm DataGrip PhpStorm CLion PyCharm GoLand RubyMine; do
    rm -rf ~/.config/$product*/eval 2> /dev/null
    rm -rf ~/.config/JetBrains/$product*/eval 2> /dev/null
done
```

But if not, try these:

```sh
for product in IntelliJIdea WebStorm DataGrip PhpStorm CLion PyCharm GoLand RubyMine; do
    echo "[+] Resetting trial period for $product"

    echo "[+] Removing Evaluation Key..."
    rm -rf ~/.config/$product*/eval 2> /dev/null

    # Above path not working on latest version, Fixed below
    rm -rf ~/.config/JetBrains/$product*/eval 2> /dev/null

    echo "[+] Removing all evlsprt properties in options.xml..."
    sed -i 's/evlsprt//' ~/.config/$product*/options/other.xml 2> /dev/null

    # Above path not working on latest version, Fixed below
    sed -i 's/evlsprt//' ~/.config/JetBrains/$product*/options/other.xml 2> /dev/null

    echo
done
```

Afterwards, run this command to remove user preferences:

```sh
echo "Removing userPrefs files..."
rm -rf ~/.java/.userPrefs 2> /dev/null
```

### MacOS Specific Command

If the above commands do not work on MacOS, run the following command to reset preferences:

```sh
rm -rf ~/Library/Preferences/com.apple.java.util.prefs.plist
```
