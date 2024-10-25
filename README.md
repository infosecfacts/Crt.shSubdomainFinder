## Subdomain Finder Script

This Bash function, `find_subdomains_with_crtsh`, utilizes the crt.sh SSL certificate database to find subdomains associated with a specified domain name. The function filters and lists unique subdomains by querying the crt.sh API and processing its JSON output.

### Prerequisites

- `curl`: Command line tool and library for transferring data with URLs.
- `jq`: Lightweight and flexible command-line JSON processor.
- `sed`: Stream editor for filtering and transforming text.

These tools must be installed on your system to use the function. They are commonly available on Linux and macOS, and can be installed on Windows via various methods like using Git Bash or Cygwin.

### Installation

1. Add the function to your `.bashrc` or `.bash_profile`:
   ```bash
   find_subdomains_with_crtsh(){
       local domain="$1"
       curl -s "https://crt.sh/?q=%.$domain&output=json" | \
       jq -r '.[].name_value' | \
       sed 's/\*\.//g' | \
       sort -u
   }
   ```

2. Source your profile to make the function available in your current session:
   ```bash
   source ~/.bashrc  # Or ~/.bash_profile
   ```

### Usage

To use the function, simply call it with a domain name as an argument:

```bash
find_subdomains_with_crtsh example.com
```

### Example

To find subdomains for `example.com`, you would use:

```bash
find_subdomains_with_crtsh example.com
```

Output:
```
sub1.example.com
sub2.example.com
sub3.example.com
...
```

The output will list all subdomains of `example.com` found in the crt.sh database, sorted and unique.
