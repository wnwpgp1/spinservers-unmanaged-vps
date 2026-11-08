# Unmanaged Linux VPS: Who Fixes What at 2am, Which SpinServers Plan Fits, and What Backups and cPanel Add to the Bill (Full Plan Table)

An unmanaged Linux VPS hands you root and the entire software stack above the hypervisor: OS install, kernel, patches, firewall, application, and your own backups. The provider keeps the hardware, power and network alive underneath it. SpinServers sells this as KVM virtual servers running from 2 to 32 vCPU with 4TB to 20TB of monthly transfer, on a page that advertises a starting price of **$62.00 USD per month**. Two details decide whether that works for you: port 25 is closed by default on every VPS they sell, and the uptime SLA they publish is written for dedicated servers and colocation, not for VPS.

> **Quick pick:** if you need a clean Linux box for a site, a Docker host or a staging environment and you are willing to patch it yourself, start with the smallest Simple Application Server that covers your disk and transfer needs, then confirm that tier's actual rate at checkout. At the advertised $62/month starting rate a year costs **$744** before backups, a control panel licence or extra IPs.
> 👉 [See the current SpinServers KVM VPS plans and per-tier pricing](https://bit.ly/Spinservers)

## The full KVM VPS lineup SpinServers lists

All seven configurations run a 1Gbps port and include one IPv4 plus one IPv6 address, with DDR4 memory and RAID-10 SSD storage.

| Plan | vCPU / RAM | Storage | Monthly transfer | Price (USD) | Order |
| --- | --- | --- | --- | --- | --- |
| Simple Application Server | 2 vCPU / 2GB | 40GB RAID-10 SSD | 4TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |
| Simple Application Server | 4 vCPU / 4GB | 80GB RAID-10 SSD | 8TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |
| Simple Application Server | 6 vCPU / 8GB | 120GB RAID-10 SSD | 8TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |
| Simple Application Server | 8 vCPU / 8GB | 160GB RAID-10 SSD | 10TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |
| Simple Application Server | 12 vCPU / 12GB | 160GB RAID-10 SSD | 10TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |
| Simple Application Server (Intel Xeon) | 16 vCPU / 16GB | 320GB RAID-10 SSD | 15TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |
| Advanced Application Server (Intel Xeon) | 32 vCPU / 32GB | 500GB SSD | 20TB | from $62.00/mo* | [Check price](https://bit.ly/Spinservers) |

\*$62.00/month is the starting price the KVM VPS page displays, not a per-tier price. SpinServers does not print a price next to each configuration, so the number for the tier you want has to come from checkout or a presales ticket. I am not going to guess at the ladder.

Three things the table tells you without any prices. Memory climbs 2, 4, 8, 8, 12, 16, 32GB. The jump from 8 vCPU to 12 vCPU buys cores and RAM only, since both tiers sit at 160GB and 10TB, so if your bottleneck is disk or transfer, that step is wasted money. Real headroom on storage starts at the 16 vCPU tier with 320GB and 15TB.

## What "unmanaged" takes off the provider's plate

hosting.com states the split cleanly: you manage everything above the operating system, including OS choice and updates, security patching, your software and your own backups unless you buy theirs; they manage the physical hardware, power, network and datacenter. Hostwinds words the same boundary in a way that is harder to misread. Its unmanaged VPS services "do not come with any technical, management, or administrative support," and what the company guarantees is that your VPS can start up and is "functional" with power, networking and the connection back to Hostwinds.

Translated into tickets: a failed disk, a dead uplink or a host node that will not boot is their problem. A broken nginx config, a PHP extension that will not compile, a MySQL table that needs recovering, a hacked WordPress install: yours. InMotion's comparison table spells out the support scope of its self-managed tier as "24/7 human support for your hardware, network, and data center only."

Root access is what you are buying in exchange. It lets you load a custom ISO, run your own kernel modules, deploy Docker and docker-compose stacks, write iptables rules, and install daemons a shared host would never allow. It does not buy you a person to debug the result.

One nuance worth internalising before you shop: root is not the line between managed and unmanaged. InMotion's managed VPS plans also ship full root and SSH access, while hosting.com's managed plans do not. The dividing line is who patches the OS and who answers the ticket, not who holds the password.

## Two SpinServers details that change the decision

### Port 25 is closed on every VPS by default

The KVM VPS page carries the same note on all seven configurations: to prevent IP abuse, port 25 (SMTP) is closed by default, and you must open a ticket with a justification to have it unblocked. The company reserves the right to deny the request for any reason.

If your application sends password resets, order confirmations or invoices straight from the box, outbound mail will fail on day one. Two ways around it: a third-party transactional email relay, or a ticket before you migrate. Anyone planning to run a mail server on a SpinServers VPS should get a yes in writing first, because the policy allows a no.

### The published SLA is scoped to dedicated servers and colocation

SpinServers' SLA document commits to 99.99% monthly uptime for "the network and power delivered to eligible dedicated servers," with service credits from 10% at 99.95–99.99% up to 40% below 99.80%, calculated on the monthly recurring charge. The same document says its dedicated servers are unmanaged unless otherwise stated, and that the commitment "does not cover the availability of the operating system, applications, customer configurations, or other server-management functions." Colocation gets a separate 99.999% power and network commitment.

Nothing there promises a VPS buyer a specific uptime figure. If a guaranteed number matters to your contract or your customers, ask presales for the VPS commitment in writing before paying. Also read the credit table for what it actually is: at 99.99% you can be down for up to four minutes in a month and receive nothing, and credits are never cash refunds and never exceed one month's fee.

👉 [Compare the SpinServers KVM VPS tiers and current rates](https://bit.ly/Spinservers)

## What the bill looks like after month one

The sticker rate is never the whole number. Four items get added to an unmanaged server, and only one of them is optional in practice.

**Backups.** The KVM VPS page does not list backups among the included features. For scale, Hostwinds prices nightly backups at $1 a month plus $0.03 per GB, which works out to $1.90/month on a 30GB server and $5.80/month on a 160GB one. That is Hostwinds' rate, not SpinServers', but it shows how the charge scales with disk: the bigger the plan, the more the backup line grows. Ask what SpinServers charges before you assume snapshots are free.

**Control panel.** cPanel is not included and needs its own licence. Hostwinds puts the practical floor for a cPanel server at 1 CPU, 2GB RAM and 50GB of disk, which means the entry SpinServers tier sits right at the minimum, and the licence is a recurring cost on top of the VPS. If you do not specifically need cPanel's interface for clients, a bare server with SSH and a config management script is cheaper and faster to rebuild.

**Extra IPs.** One IPv4 and one IPv6 come with every tier. Additional IPv4 addresses are typically billed monthly and are not priced on the page.

**Management, if you decide you want it.** At the budget end the gap is smaller than people expect. Hostwinds lists a 1 CPU / 1GB / 30GB / 1TB server at $4.99/mo on its unmanaged page, and the same specification at $7.14/mo (regular $10.99) on its Linux VPS page that also sells full management. A couple of dollars a month separates self-managed from managed at that size, and what the managed side adds is documented: OS and panel updates, monitoring, security patching, proactive support and daily backups included rather than optional.

Do the arithmetic on the SpinServers starting rate and a year of the entry tier is $744 in base fees. Add backups, a panel licence and an extra IP and you are budgeting meaningfully above that. The licence alone can rival a small VPS.

## Who should not buy unmanaged

Three reader profiles should stop here and buy managed instead, and the providers say so themselves.

You are moving off shared hosting and want to keep cPanel. hosting.com recommends a managed VPS for exactly this case and offers free migration of existing sites. InMotion bundles cPanel and WHM, maintained, on its managed plans, plus free migration. On an unmanaged box you install and license the panel yourself and migrate your own sites.

You have no Linux command-line experience. hosting.com's own advice is to pick managed if you would rather the provider handle OS updates, patching and a control panel. An unmanaged VPS will run fine until the first thing breaks, and then you are the entire support organisation.

You need application-level fixes at odd hours. Unmanaged support stops at hardware and network. If a payment plugin throws errors at 2am and you want a human to look at it, that is a managed contract, not a root password.

There is a fourth case specific to SpinServers: you need outbound SMTP from the server itself. With port 25 closed by default and reopening subject to approval, a mail server is the wrong workload for this platform unless you clear it in advance.

## How the rest of the market prices unmanaged Linux VPS

These are published configurations and rates from other providers, included for price anchoring only.

| Provider | Plan | vCPU / RAM / storage | Transfer | Price |
| --- | --- | --- | --- | --- |
| Hostwinds | Unmanaged Linux | 1 CPU / 1GB / 30GB | 1TB | $4.99/mo |
| Hostwinds | Unmanaged Linux | 2 CPU / 4GB / 75GB | 2TB | $18.99/mo |
| Hostwinds | Unmanaged Linux | 4 CPU / 8GB / 150GB | 3TB | $38.99/mo |
| BlastVPS | VPS-Basic (Ryzen 9 3900X, KVM) | 2 vCore / 4GB / 40GB NVMe | Unmetered | $10.99/mo |
| BlastVPS | VPS-Pro | 4 vCore / 8GB / 80GB NVMe | Unmetered | $29.99/mo |
| InMotion Hosting | Self-Managed VPS | 8 vCPU / 16GB / 260GB NVMe | Unmetered | €31.90/mo on a 24-month term, renews at €84.10/mo |

The budget end of this market is $5 to $11 a month for 1 to 4 vCPU and 1 to 4TB of transfer. SpinServers' advertised $62 starting point sits a bracket or two above that, and what the money buys is transfer and core count: 4TB to 20TB, a 1Gbps port, an IPv6 address, and room to run a real application stack rather than a single small site. If all you need is a 1GB box for a brochure site, that capacity is wasted. If you push several terabytes a month, the 1TB to 3TB caps on the cheap tiers become the binding constraint and the effective cost per delivered gigabyte flips.

Disk type is the other visible difference. The budget tiers above advertise NVMe; SpinServers' VPS line lists RAID-10 SSD. For a database-heavy workload NVMe has the edge on latency; for an app server moving a lot of traffic, port speed and transfer allowance matter more than the storage bus.

## Choosing a tier by workload

**One low-traffic site plus cron jobs and a small database:** the 2 vCPU / 2GB / 40GB tier, provided you are not stacking cPanel on it. Hostwinds' own cPanel minimum is 2GB, so a panel plus a database plus PHP leaves very little room. Drop the panel and this tier is comfortable.

**Docker, CI runners, staging environments:** 4 to 8 vCPU. Budget RAM per container rather than per core, and remember snapshots and rebuilds are your responsibility here. The 8 vCPU / 8GB / 160GB tier is the sweet spot before the plateau.

**Agency or multi-tenant hosting with several client sites:** the 16 vCPU / 16GB / 320GB / 15TB tier, or the 32 vCPU Advanced tier if you are consolidating many sites onto one box. Skip the 12 vCPU step unless you specifically need cores and memory and nothing else.

**Mail server:** none of these tiers, until port 25 is confirmed open.

**Anyone who wants updates, patching and a panel handled:** not this product. Buy managed.

## Before you pay, confirm six things

1. **The per-tier price and the billing term.** The page advertises a $62/month starting rate; longer terms, promotional pricing and renewal rates are not published on the VPS page.
2. **Whether backups are included**, and the monthly price if they are not, scaled to your disk size.
3. **The VPS uptime commitment in writing.** The published SLA covers dedicated servers and colocation.
4. **The cost of extra IPv4 addresses**, since one of each family is the included allocation.
5. **Port 25**, if anything on the server sends mail.
6. **Refund and cancellation terms.** They are not stated on the pages reviewed here, so get them from presales before the first payment rather than after.

Run those six questions past presales and you will know more about the deal than the pricing page tells you. If the answers line up with your workload, the transfer allowance and core counts are the reason to pick this over a $5 box.

👉 [Start with the SpinServers KVM VPS plan list and current pricing](https://bit.ly/Spinservers)

## FAQ

**Can I add RAM or disk later without migrating?**
It depends on the provider and SpinServers does not state its resize policy on the VPS page, so ask. The market handles this three ways: hosting.com scales individual resources on demand without a rebuild, Hostwinds upgrades you to the next tier, and InMotion supports up and down grades with the caveat that disk changes need checking. Getting this wrong means a rebuild and a migration you did not plan for.

**Is a KVM VPS the same as a dedicated server?**
No. KVM gives you a virtual machine with dedicated vCPU and RAM allocations on shared physical hardware, which isolates you from other tenants but still shares the bus underneath. SpinServers also sells dedicated servers, which the SLA describes as unmanaged unless otherwise stated. Move up when a single VM's ceiling becomes the limit.

**What happens if the server will not boot?**
That is inside the provider's scope. Hostwinds defines its obligation as keeping the VPS able to start and function with power, networking and the connection to its network; InMotion covers hardware, network and datacenter around the clock. Recovery of your data, your OS and your configuration is your side of the line, which is why an off-box backup matters more on unmanaged hosting than anywhere else.
