# SySaSir

> [Leer en español](/README-es.md)

Collection of scripts, programs, and abundant documentation developed throughout [ASIR](https://todofp.es/que-estudiar/loe/informatica-comunicaciones/admin-sist-informaticos-red.html) - IT Certification.

Contributions are welcome, so feel free to engage sending PRs, sharing your own utilities or tweaking ours, starting issues and discussions, etc.

As we cover a wide array of software domains, technologies, and specialized undertakings (sysadmin, devops, db-admin, netadmin, pentesting...), the chart below should provide a concise overview of the relevant utilities within this repo.

For more information see [FAQs](/FAQs.md) and [CONTRIBUTING](#).


<details>
<summary>Table of Contents</summary>

- [SySaSir](#sysasir)
  - [Utilities](#utilities)
    - [Showcase](#showcase)
      - [001 - `recon_nmap.sh`](#001---recon_nmapsh)

</details>


## Utilities

> WIP

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


<br><table>
    <thead>
        <tr>
            <th>Platform</th>
            <th>Domain</th>
            <th>Specialty</th>
            <!-- <th>Language</th> -->
            <th>Concept</th>
            <th>Utility</th>
            <th>ID</th>
            <th>Status</th>
        </tr>
    </thead>
        <tr>
            <td rowspan=4>N/A</td>
            <td rowspan=4>Databases</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Infraestructure</td>
            <td><b>Server/Client</b>: Docker, Linux, Termux, Windows, WSL <br><b>IDEs</b>: Neovim (LSPs + DAPs),  VSCode SQLTools</td>
            <td><a href="https://github.com/pabloqpacin/ASIR/blob/main/ASIR%2B/MySQL/MySQL-alt-CLI.md">MySQL-alt-CLI.md</a></td>
            <td>101</td>
            <td>⚠️</td>
        </tr>
        <tr>
            <td>User Management</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>SQL</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=2>N/A</td>
            <td rowspan=4>OSs</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Nested Virtualization</td>
            <td><b>WSL</b>: Windows guest on Linux/Windows host
            <br><b>Hypervisors</b>: Hyper-V, KVM, VirtualBox, VMware</td>
            <td>...</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>Linux</td>
            <td>Arch</td>
            <td>System Installation & Desktop Configuration</td>
            <td>...</td>
            <td></td>
            <td>⚠️</td>
        </tr>
        <tr>
            <td rowspan=1>Windows</td>
            <td>PowerShell</td>
            <td>...</td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=2>N/A</td>
            <td rowspan=3>Networking</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Subnetting</td>
            <td>...</td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>Linux</td>
            <td>Network Enumeration</td>
            <!-- <td>Bash</td> -->
            <td>Contextual menu for nmap scanning</td>
            <td><a href="/linux/scripts/recon_nmap.sh">recon_nmap.sh</a></td>
            <td>001</td>
            <td>✅</td>
        </tr>
        <tr>
            <td rowspan=4>N/A</td>
            <td rowspan=4>Web</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>HTML</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>CSS</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>JavaScript</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=2>N/A</td>
            <td rowspan=2>Misc.</td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>Git</td>
            <td><b>Git 101</b>: create repo (local|remote), add commit & push<br><b>Git 10x</b>: rebase/squash</td>
            <td>...</td>
            <td></td>
            <td>⚠️</td>
        </tr>
        <tr>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
            <td></td>
        </tr>
    <tbody>
    </tbody>
</table>



### Showcase

#### 001 - `recon_nmap.sh`

- example run
- example screenshot
- example results: session + logs


