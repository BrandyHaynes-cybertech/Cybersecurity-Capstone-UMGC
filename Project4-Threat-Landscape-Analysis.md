# Project 4 — Cybersecurity Threat Landscape Analysis
**Course:** CMIT 495 — Cybersecurity Technology Capstone | UMGC  
**Author:** Brandy Haynes (Individual Contribution — Group Assignment)  
**Note:** This document represents the author's individual contribution to a collaborative group project.

---

## Part 1: Threat Landscape Analysis

### The Current State of Cybersecurity (2025)

In the early stages of 2025, the cybersecurity landscape reflects a rapidly evolving world shaped largely by the explosive growth of the Internet of Things (IoT). Technological advancement is far outpacing the effective implementation of security controls, leaving organizations vulnerable to increasingly sophisticated threats.

IoT devices are now embedded into nearly every fabric of everyday life — whether personal, business, or critical infrastructure. From wearable health monitors and smart home systems to autonomous self-driving vehicles, these interconnected devices have created a nearly immeasurable digital ecosystem aimed at enhancing convenience while simultaneously weakening security by leaving behind digital fingerprints that threat actors can trace and exploit.

Combined with rapid advancements in cloud computing, artificial intelligence, machine learning, and automation, this technological evolution serves as a stark reminder that **innovation without robust security measures creates a far greater risk than reward** in today's hyper-connected digital age.

---

### How the Threat Landscape Changed: 2020–2025

Between 2020 and 2025, the cybersecurity landscape underwent dramatic changes that fundamentally reshaped the threat environment.

**The COVID-19 Catalyst**
As the COVID-19 pandemic disrupted the global economy, organizations were forced to rapidly adopt remote work — creating an unprecedented and long-term reliance on cloud infrastructure. This rapid transition was further accelerated by disruptions to the global supply chain, placing additional pressure on organizations to digitalize operations quickly. Organizations rushed to migrate sensitive data and critical systems to the cloud, often without thorough security oversight, introducing a slew of new vulnerabilities.

---

### The Rise of Supply Chain Attacks

Among the most impactful changes to the cybersecurity landscape between 2020 and 2025 was the sharp rise in **supply chain attacks** — quickly becoming the preferred method for both nation-state and cybercriminal groups.

Threat actors realized that compromising a single trusted vendor could provide easy access to hundreds or even thousands of downstream organizations.

#### Case Study 1 — SolarWinds (2020)

The SolarWinds supply chain attack remains one of the most significant cyberattacks in modern history. Attackers inserted malicious code known as **SUNBURST** into software updates for the widely used SolarWinds Orion platform.

**Impact:**
- Approximately **18,000 organizations** worldwide unknowingly downloaded the compromised update
- Victims included Fortune 500 companies, U.S. Federal agencies, and government entities across the globe
- The attack went **undetected for several months**, providing attackers with long-term access to sensitive systems and data
- Demonstrated how a single compromised vendor could exponentially amplify a breach across thousands of interconnected networks

#### Case Study 2 — MOVEit Supply Chain Attack (2023)

In 2023, the **Clop ransomware group** exploited a zero-day vulnerability within MOVEit Transfer — a widely used file transfer tool heavily relied upon across finance, education, healthcare, and government sectors where secure file sharing is a regulatory requirement.

**Impact:**
- Hundreds of organizations breached through a single exploit
- High-value target due to MOVEit's role as critical infrastructure for secure data transfer
- Demonstrated that threat actors increasingly focus on widely used tools and platforms that act as critical infrastructure for countless organizations

---

### Key Takeaways

The SolarWinds and MOVEit attacks, while years apart, illustrate the same fundamental weakness in modern cybersecurity — **dependence on third-party vendors for essential business functions**.

In today's hyper-connected world, organizations no longer operate in isolated environments. They rely on extensive ecosystems of software suppliers, service providers, and cloud platforms. This interconnected ecosystem enhances operational efficiency but simultaneously amplifies the impact of a single breach across the entire supply chain.

**In 2025, supply chain attacks remain a dominant threat.** Attackers are actively scanning for:
- Portable third-party platforms
- Insecure software updates
- Weak links in vendor ecosystems

This ongoing trend underscores the critical importance of:
- **Third-party risk management**
- **Vendor security audits**
- **Continuous monitoring**

---

### Predicted Exploit Vectors & Vulnerabilities

Cyber threat actors are expected to continue exploiting established weaknesses while shifting focus to newer technologies:

- **Cloud Misconfigurations** — remain the most common vulnerability as organizations struggle to properly secure increasingly complex multi-cloud environments. Mismanaged access controls, overpermissioned accounts, and exposed storage buckets provide attackers with easy access to critical data
- **IoT Vulnerabilities** — rapidly expanding attack surface as IoT devices continue to proliferate without adequate security controls
- **AI-Powered Attacks** — threat actors leveraging machine learning to automate and scale attacks, identify vulnerabilities faster, and evade traditional defenses

---

## References

1. CISA. SolarWinds Supply Chain Attack. https://www.cisa.gov/news-events/alerts/2020/12/17/cisa-emergency-directive-21-01
2. U.S. Government. MOVEit Transfer Critical Vulnerability. https://www.cisa.gov/known-exploited-vulnerabilities-catalog
3. NIST. National Vulnerability Database. https://nvd.nist.gov/
