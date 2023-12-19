# sys_asir

> [Leer en español](/README-es.md)

Collection of scripts, programs, and abundant documentation developed throughout [ASIR](https://todofp.es/que-estudiar/loe/informatica-comunicaciones/admin-sist-informaticos-red.html) - IT Certification.

Contributions are welcome, so feel free to engage sending PRs, sharing your own utilities or tweaking ours, starting issues and discussions, etc.

As we cover a wide array of software domains, technologies, and specialized undertakings (sysadmin, devops, db-admin, netadmin, pentesting...), the chart below should provide a concise overview of the relevant utilities within this repo, and some are actually showcased further below.

For more information see [FAQs](/FAQs.md) and [CONTRIBUTING](#).


<details>
<summary>Table of Contents</summary>

- [sys\_asir](#sys_asir)
  - [Utilities](#utilities)
    - [N-001 - recon\_nmap.sh](#n-001---recon_nmapsh)

</details>


## Utilities

<details>
<summary>DELETE ME</summary>

```yaml
Status:
    - ✅ : should be alrightie
    - ⚠️ : use with caution
    - ❌ : underdeveloped

Neovim:
    # https://github.com/pabloqpacin/dotfiles
    - LSPs: lsp-zero    # https://github.com/VonHeikemen/lsp-zero.nvim
    - DAPs: nvim-dap    # https://github.com/mfussenegger/nvim-dap
        # https://microsoft.github.io/language-server-protocol
        # https://microsoft.github.io/debug-adapter-protocol


Recommendations:
    - Verify: Read them scripts before using them dawg
```

</details>


<table>
    <thead>
        <tr>
            <th>Domain</th>
            <th>Specialty</th>
            <!-- <th>Language</th> -->
            <th>Concept</th>
            <th>Utility</th>
            <th>Status</th>
        </tr>
    </thead>
        <tr>
            <td rowspan=3>Databases</td>
            <td>Server/Client + IDEs</td>
            <!-- <td>- Docker, Linux, Termux, Windows, WSL <br>- Neovim,  VSCode SQLTools</td> -->
            <td><a href="https://github.com/pabloqpacin/ASIR/blob/main/ASIR%2B/MySQL/MySQL-alt-CLI.md">MySQL-alt-CLI.md</a></td>
            <td>⚠️</td>
        </tr>
        <tr>
            <td>Users & Permissions</td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>SQL</td>
            <td>DCL DDL DML DQL TCL</td>
            <!-- <td><a href="/sql/">repaso*.sql</a></td> -->
            <td>...</td>
            <td>⚠️</td>
        </tr>
        <tr>
            <td rowspan=3>OSs</td>
            <td>Nested Virtualization</td>
            <td>- WSL guest on any host<br>- VirtualBox, Hyper-V, KVM</td>
            <td>...</td>
            <td></td>
        </tr>
        <tr>
            <td>Arch</td>
            <td>Installation & Configuration</td>
            <td>...</td>
            <td>⚠️</td>
        </tr>
        <tr>
            <td>PowerShell</td>
            <td>...</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=2>Networking</td>
            <td>Subnetting</td>
            <td>...</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Network Enumeration</td>
            <!-- <td>Bash</td> -->
            <td>CLI scanning menu</td>
            <td><a href="/linux/scripts/recon_nmap.sh">recon_nmap.sh</a></td>
            <td>✅</td>
        </tr>
        <!-- <tr>
            <td rowspan=3>Web</td>
            <td>HTML</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>CSS</td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>JavaScript</td>
            <td></td>
            <td></td>
            <td></td>
        </tr> -->
        <tr>
            <td rowspan=1>MISC.</td>
            <td>Git</td>
            <td><code>init</code> <code>add</code> <code>commit</code> <code>push</code> <code>rebase</code></td>
            <td>...</td>
            <td>⚠️</td>
        </tr>
        <!-- <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr> -->
    <tbody>
    </tbody>
</table>

---

### N-001 - [recon_nmap.sh](/linux/scripts/recon_nmap.sh)


<details>
<summary>Click here to read the very script</summary>

```bash
#!/bin/bash

echo -e "\n----###############################################################----"
echo -e "#########~~~~~{     R3C0N NM4P v1.1  by @pabloqpacin    }~~~~~#########"
echo -e "----###############################################################----\n"

# Session addresses & target_list optional argument
net=$(ip route | grep 'src' | awk '{print $1}' | head -n 1)
ip=$(ip route get 1 | awk '{print $7}')
targets=("_gateway" "localhost" "scanme.nmap.org")

echo -e "#  NOTE: Run './recon_nmap.sh target_list.txt' to add extra targets.  #\n"
if [ -n "$1" ]
    then target_list="$1"
    while IFS= read -r line
        do targets+=("$line")
    done < "$target_list"
fi

# Logging scans
log_dir=/tmp/recon; mkdir $log_dir &>/dev/null
log_name=$(date +%Y-%m-%d)
log_temp="$log_dir/scan.txt"
log="$log_dir/$log_name.txt"

# Determine whether to 'grc' -- https://github.com/garabik/grc
if command -v grc &>/dev/null
    then nmap="grc nmap"
    else nmap="nmap"
fi

# Fetch interfaces
read -p "Scan network interfaces? [y/N] " opt
if [[ $opt == "Y" || $opt == "y" ]]
then
    $nmap --iflist
fi

# 0)
function set_target {
    while true
        do read -p "Set new target domain or IP (or press Enter to exit): " target_value
        if [ -z "$target_value" ]; then
            break
        fi
        targets+=("$target_value")
    done
}

# 1)
function open_target {
    $nmap --open $1 -oN $log_temp
}

# 2)
function ping_scan_target {
    $nmap -sP $1 -oN $log_temp
}

# 3)
function TCP_scan_target {
    $nmap -sT $1 -oN $log_temp
}

# 4)
function SYN_scan_target {
    sudo $nmap -sS $1 -oN $log_temp
}

# 5)
function Version_scan_target {
    $nmap -sV $1 -oN $log_temp
    # script -qc "$nmap -sV $1" -a $log; sed_del
}

# MORE: nmap scripts...

# 8)
function Sam_scan {
    $nmap -p- -sCV -Pn $1 -oN $log_temp
}

# 9)
function custom_command {
    read -p "Enter the command to be run: " custom
    (eval "$custom")
}

# *)
function exit_script {
    read -p "Delete $log_dir? [Y/n] " opt
    if [[ $opt == "Y" || $opt == "y" || $opt == "" ]]
        then rm -rf /tmp/recon
    fi
    exit 0
}

# Determine target for every scan -- https://www.gnu.org/software/bash/manual/html_node/Arrays.html; https://opensource.com/article/18/5/you-dont-know-bash-intro-bash-arrays
function target_prompt {
    read -p "Enter target IPv4, domain name or keyword (net, ip, t1 t2 ...): " target_answer

    if [[ $target_answer == t* ]]
        then local target_index="${target_answer#t}"
        target_scan="${targets[target_index - 1]}"
    else
        declare -A target_mapping=(
            [ip]="$ip"
            [net]="$net"
        )

        if [ -n "${target_mapping[$target_answer]}" ]
            then target_scan="${target_mapping[$target_answer]}"
            else target_scan="$target_answer"
        fi
    fi
    echo -e "#######################################################################\n"
}

# Main loop
while true
do
    if [[ -e $log_temp ]]
        then cat $log_temp >> $log; echo "---" >> $log
    fi

    echo -e "\n#######################################################################"
    echo -e "# Scan log ................................. $log"
    echo -e "# Active subnet ............................ $net"
    echo -e "# Active IP................................. $ip"
    echo -e "# Known targets:"
    for i in "${!targets[@]}"
        do echo -e "\tt$((i+1)) ................................. ${targets[i]}"
    done

    echo -e "\nActions available:"
    echo -e "\t0) Set new target."
    echo -e "\t1) Scan open ports ----------------> nmap --open ..."
    echo -e "\t2) Ping-scan target ---------------> nmap -sP ..."
    echo -e "\t3) TCP-scan target ----------------> nmap -sT ..."
    echo -e "\t4) SYN-scan target ----------------> sudo nmap -sS ..."
    echo -e "\t5) App Version scan ---------------> nmap -sV ..."
    # echo -e "\t6)   *WIP*                          --script"
    # echo -e "\t7)   *WIP*                          --script"
    echo -e "\t8) Sam scan -----------------------> nmap -p- -sCV -Pn -T4 ..."
    echo -e "\t9) Custom command."
    echo -e "\tl) Clear screen."
    echo -e "\t*) Exit.\n"
    
    read -p "Select action: " opt
    # read -p "Enter target: " target_scan

    case $opt in
        "0") set_target ;;
        "1") target_prompt; open_target $target_scan ;;
        "2") target_prompt; ping_scan_target $target_scan ;;
        "3") target_prompt; TCP_scan_target $target_scan ;;
        "4") target_prompt; SYN_scan_target $target_scan ;;
        "5") target_prompt; Version_scan_target $target_scan ;;
        "8") target_prompt; Sam_scan $target_scan ;;
        "9") custom_command ;;
        "l") clear ;;
        "*") exit_script ;;
    esac

done
```
</details>

- As for **USAGE**, you may run the file as any other bash script:

```bash
$ .recon_nmap.sh
```
- It accepts one argument (`$1`). It should be a text file with a single IPv4 or domain name in every line.

```bash
$ cat target_list.txt
inlanefreight.com
8.8.8.8

$ .recon_nmap.sh target_list.txt
```

- As for RESULTS, this is the actual contextual menu for `nmap` scans. It features network information, a targets shortlist, stealthy logging and coloured output if [grc](https://github.com/garabik/grc) is installed. 

```log
#######################################################################
# Scan log ................................. /tmp/recon/2023-10-04.txt
# Active subnet ............................ 192.168.1.0/24
# Active IP................................. 192.168.1.38
# Known targets:
	t1 ................................. _gateway
	t2 ................................. localhost
	t3 ................................. scanme.nmap.org

Actions available:
	0) Set new target.
	1) Scan open ports ----------------> nmap --open ...
	2) Ping-scan target ---------------> nmap -sP ...
	3) TCP-scan target ----------------> nmap -sT ...
	4) SYN-scan target ----------------> sudo nmap -sS ...
	5) App Version scan ---------------> nmap -sV ...
	8) Sam scan -----------------------> nmap -p- -sCV -Pn -T4 ...
	9) Custom command.
	l) Clear screen.
	*) Exit.

Select action: 2
Enter target IPv4, domain name or keyword (net, ip, t1 t2 ...): net
#######################################################################
```

<!-- - example run
- example screenshot
- example results: session + logs -->

- Sample PICTURE:

![recon_nmap-01](/img/recon_nmap-01.png)

---

