# Answers to Part 3

Add your answers to the questions in Part 3, Step 2 below. 

## Vulnerability Remediation:
### Vulnerability 1: 
1. Which package or library are you addressing? 

PyYAML 5.1 from requirements.txt. Trivy flagged it as critical in the code scan.

2. Which CVE is linked to this vulnerability? 

CVE-2020-1747. In PyYAML versions before 5.3.1, loading YAML with full_load() or FullLoader isn't actually safe. If someone sends the app a YAML file that uses the python/object/new tag, they can get it to run their own code on the server. It's an insecure deserialization problem.

3. What remediation steps do you suggest?

Upgrade PyYAML to 5.4 or newer in requirements.txt (5.3.1 didn't fully fix the issue) and use yaml.safe_load() when loading YAML that comes from users.

### Vulnerability 2:
1. Which vulnerability are you addressing?

Pillow 9.4.0, which is installed in the container image. Docker Scout flagged it as critical with a CVSS score of 9.3.

2. Which CVE is linked to this vulnerability?

CVE-2023-50447. Pillow's ImageMath.eval() function uses Python's eval() behind the scenes. In versions before 10.2.0, if an attacker can control the environment argument that gets passed to it, they can inject Python code and run it on the server.

3. What remediation steps do you suggest? 

Upgrade Pillow to 10.2.0 or newer in requirements.txt, then rebuild the image and run the scan again to make sure the vulnerability is gone.