# Reconator
Reconator is a powerful Bash script designed to automate the process of domain reconnaissance and scanning. It integrates various tools such as `subfinder`, `httpx`, `naabu`, `dirsearch`, `nuclei`, `gau`, `uro`, `katana`, and more to provide a comprehensive analysis of the target domain(s). The script offers flexibility through customizable flags and supports both single domains and lists of domains, making it an essential tool for penetration testers and security researchers.

## Prerequisites

Before running the script, ensure that the following tools are installed and accessible in your system's PATH:

- [Subfinder](https://github.com/projectdiscovery/subfinder)
- [Httpx](https://github.com/projectdiscovery/httpx)
- [Naabu](https://github.com/projectdiscovery/naabu)
- [Dirsearch](https://github.com/maurosoria/dirsearch)
- [Nuclei](https://github.com/projectdiscovery/nuclei)
- [Gau](https://github.com/lc/gau)
- [Uro](https://github.com/s0md3v/uro)
- [Katana](https://github.com/projectdiscovery/katana)
- [SecretFinder](https://github.com/m4ll0k/SecretFinder)
- [anew](https://github.com/tomnomnom/anew)
- [jq](https://stedolan.github.io/jq/)

## Installation

To install Reconator, follow these steps:

 - **Clone the Repository:**

```bash
   git clone https://github.com/Entit-y/Reconator.git
```

## Usage

Navigate to the cloned repository and use the following command to run the script:

```bash
./reconator
```

### Script Workflow

The script performs the following tasks in sequence:

1. **Prompt User for Input:**
    - Enter the target domain or a file path containing a list of domains.
    - Specify the directory where output files will be saved.
    - Choose whether to use custom flags for the tools.
    
2. **Domain Cleaning:**
    - If a file with domains is provided, it cleans and sorts the domains.
    
3. **Subdomain Discovery:**
    - **Subfinder:** Discovers subdomains.
    - **crt.sh:** Enhances subdomain discovery with CRT data.
    
4. **HTTP Probing:**
    - **Httpx:** Checks for alive subdomains.
    
5. **Port Scanning:**
    - **Naabu:** Scans for open ports.
    
6. **Directory Bruteforcing:**
    - **Dirsearch:** Scans directories.
    
7. **Vulnerability Scanning:**
    - **Nuclei:** Scans for known vulnerabilities.
    
8. **Parameter Extraction and Filtering:**
    - Extracts and filters parameters using `gau` and `uro`.
    
9. **JavaScript Files and Secret Extraction:**
    - Finds JavaScript files and extracts potential secrets.
    
10. **Recursive Crawling:**
    - **Katana:** Performs recursive crawling for additional discovery.
    
11. **Process Katana Output:**
    - Processes the output for files and secrets.
    
12. **Directory Search with Extensions:**
    - Extends directory searching to specific file types.

### Customization

#### Custom Flags

When prompted, you can enter custom flags for each tool. If no custom flags are provided, default flags will be used:

- **Subfinder:** `-all -recursive`
- **Httpx:** `-ports 80,443,8080,8000,8888 -threads 200`
- **Naabu:** `-c 50 -nmap-cli 'nmap -sV -sC'`
- **Dirsearch:** `-x 500,502,429,404,400 -R 5 --random-agent -t 100 -F`
- **Nuclei:** `-c 70 -rl 200 -fhr -lfa -no-mhe`
- **Katana:** `-d 5 -ps -pss waybackarchive,commoncrawl,alienvault -kf -jc -fx -ef woff,css,png,svg,jpg,woff2,jpeg,gif,svg`

#### Output Directory

Specify the directory where you want all output files to be saved. If no directory is specified, the current working directory is used by default.

### Resuming Scans

The script can resume from the last completed step in case of interruption. It stores the last completed step in a file named `last_step.txt` in the output directory. This ensures that you can continue without repeating already completed tasks.

### Error Handling

The script is equipped with error handling features. If an error occurs, it will log the error message and exit gracefully. Errors are also logged to `error.log` in the output directory.

### Signal Handling

The script handles the following signals:

- `SIGQUIT (Ctrl+\)`: Skips the current tool and proceeds to the next.
- `SIGINT (Ctrl+C)`: Exits the script gracefully.

## Troubleshooting

- **Command Not Found:** Ensure all required tools are installed and accessible in the system's PATH.
- **Empty Output Files:** Verify the input domain or domain list file. Check internet connectivity.
- **Permission Issues:** Run the script with sufficient permissions to read/write the specified directories.
