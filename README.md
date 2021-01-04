## coyote

iOS telemetry/research ITW devices

Reporting exploited vulnerabilities in the wild is a complex process where each side uses their business or personal interests. Attaching evidence of exploitation, also involves sharing private Threat intelligence information with a software vendor. A company which has more resources and could act in bad faith. For this reason, many companies and researchers don't disclose vulnerabilities until sufficient information has been gathered about attackers (targets, techniques, C&C, etc). It is difficult to establish a relationship of trust where there is so much work involved and so many opposing interests. There is only one thing in common, users of this software and their security and/or privacy.

One of the viable solutions but one that needs years of research and development is [zero-knowledge (ZK) proofs](https://en.wikipedia.org/wiki/Zero-knowledge_proof). As described in **Trail of Bits's blog** [Reinventing Vulnerability Disclosure using Zero-knowledge Proofs](https://blog.trailofbits.com/2020/05/21/reinventing-vulnerability-disclosure-using-zero-knowledge-proofs/). Questions remain to be answered about how feasible this is in practice. Among other things, distribute updated builds with ZKP statements and how non-deterministic areas could be evaluated. It is certainly a fascinating work in progress.

Other options like #FreeTheSandbox are actually a bad idea that only increases the attack surface. **The cost of downgrading end-user security in general to improve threat detection is nonsense.**

**Suitable device must have**: Hardware tracing enabled, Hardware-assisted memory sanitizers, memory and file system dumps. But so far the most suitable solution is to have virtualization in place (lightweight iOS VM on-device) with hardware isolation, security extensions, virtio devices, passthrough, apfs/memory snapshots, etc. Apple provides [Hypervisor.framework](https://developer.apple.com/documentation/hypervisor) and the Virtualization Extensions are expected to appear on new **A14** devices, as well as exposed entitlements to users. If this is the case, it is the best option to have a telemetry/research device where Hypervisor Instrospection or agentless sandbox solutions (to note some) are feasible for end users. If not, **Apple could expose these in future Security Research Devices intended for this type of analysis**. Which would be great too, especially if there is the possibility of sharing Apple signed memory and file system snapshots (or simply a whole VM) with Apple for a peer review, either at the same time of evaluation or before a publication/disclosure.

## Apple Security Research Device Program

Although [SRD](https://developer.apple.com/programs/security-research-device/) make triage work on various aspects of an exploit chain somewhat easier, these devices are not intended for this use. Testing on a device that is rare or unusual (different kernel, boot flags, OS builds, different restrictions/sandbox in place, etc.) raises all the alarms for an attacker, and stops next steps in an exploit chain to prevent forensic analysis or any replay attempt. [Scout agents or validators](https://citizenlab.ca/2014/06/backdoor-hacking-teams-tradecraft-android-implant/) are specifically designed for this task. Some are just designed to fingerprint browsers (eg: WEBGL_debug_renderer_info, canvas, Fonts, etc.) just before the initial step in the [encrypted exploit delivery](https://github.com/MRGEffitas/Ironsquirrel).

Additionally it can put you in a bad place **legally** if ~~internal builds (symbols, beta firmwares, tools, etc) are leaked~~ by attackers or they use this to improve their knowledge or tools. In short, under no circumstances you are going to analyze something that escapes your expertise in a device that is not your property and which you can't confine or control.

## References

[1] https://www.haaretz.com/israel-news/.premium-with-israel-s-encouragement-nso-sold-spyware-to-uae-and-other-gulf-states-1.9093465

> To prevent intelligence information from leaking out, Pegasus “commits suicide” if a device with the software enters five countries: Israel, Iran, Russia, China and the United States. So if a Saudi citizen whose cellphone has been infected with the spyware lands in Moscow, his device recognizes that it’s in Russia and the software is wiped from the phone. The purpose is to avoid getting in trouble with states that will not tolerate espionage within their borders, such as China and the United States, or in the case of Iran, to avoid exposing secrets to hostile countries.

[2] https://www.volexity.com/blog/2020/04/21/evil-eye-threat-actor-resurfaces-with-ios-exploit-and-updated-implant/

> INSOMNIA implant; In the latest activity identified by Volexity, the Evil Eye threat actor used an open source framework called IRONSQUIRREL to launch their exploit chain

[3] Candiru leaked documents, Appendix C iOS System Supported capabilities https://www.themarker.com/embeds/pdf_upload/2020/20200902-161742.pdf

> Geo-Licensing, The product will operate in all agreed upon territories, except the restricted territories which are: US, Russia, China, Israel and Iran.

[4] Apple Sending Special iPhones to First Participants in Security Research Device Program https://www.macrumors.com/2020/12/22/apple-security-research-device-program-launches/

> Program participants have access to extensive documentation and a dedicated forum with Apple engineers for collaborative purposes. 

