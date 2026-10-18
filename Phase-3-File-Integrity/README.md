# Phase 3: File Security and Integrity Verification

## APEX Tech Forge Academy — Cybersecurity Capstone

### 1. Overview

This phase demonstrates basic file security practices in a Kali Linux virtual machine. The practical exercise focuses on restricting file permissions, generating a SHA-256 hash, and verifying file integrity using a saved checksum baseline.

### 2. Lab Environment

- **Operating system:** Kali Linux Rolling 2026.3
- **Virtualization platform:** VMware
- **User account:** `kali`
- **Sample file:** `confidential_records.txt`
- **Integrity baseline:** `baseline.sha256`

### 3. Objectives

- Create a sample file containing non-sensitive test data.
- Restrict file permissions using Linux `chmod`.
- Calculate a SHA-256 hash.
- Save the hash as a baseline.
- Verify that the file matches the saved baseline.
- Document the results as cybersecurity project evidence.

### 4. Practical Implementation

#### Step 1: Create the sample file

```bash
cd ~
printf 'APEX Tech Forge Academy sample backup record\n' > confidential_records.txt
cat confidential_records.txt
```

The file contains simulated data created for this lab exercise.

#### Step 2: Restrict file permissions

```bash
chmod 600 confidential_records.txt
ls -l confidential_records.txt
```

The expected permission string is:

```text
-rw-------
```

The `chmod 600` command gives the file owner read and write permissions while assigning no permissions to the group or other users.

#### Step 3: Generate a SHA-256 hash

```bash
sha256sum confidential_records.txt
```

This command calculates a hash based on the file's contents. The actual hash value should be recorded from the lab output.

#### Step 4: Save the checksum baseline

```bash
sha256sum confidential_records.txt > baseline.sha256
cat baseline.sha256
```

The baseline stores the checksum and filename for later comparison.

#### Step 5: Verify file integrity

```bash
sha256sum -c baseline.sha256
```

Expected result:

```text
confidential_records.txt: OK
```

This result indicates that the current file contents match the checksum recorded in the baseline.

### 5. Security Concepts Demonstrated

**File permissions:** Linux file permissions help restrict access to files. The `600` permission setting allows the owner to read and modify the file while denying ordinary group and other-user access through these permissions.

**Hashing:** SHA-256 produces a fixed-length digest of the file's contents. A change to the contents will almost certainly produce a different digest.

**Integrity verification:** Comparing a file against a previously saved checksum helps identify unexpected changes, provided the baseline is trustworthy and protected.

### 6. Security Limitations

- SHA-256 hashing does not encrypt a file.
- A checksum alone does not prove who created a file or whether its contents are trustworthy.
- The baseline should be protected separately from the file being monitored.
- A privileged administrator may still access the file despite restrictive ordinary-user permissions.

### 7. Evidence Checklist

- [x] Screenshot showing the sample file contents.
- [x] Screenshot showing the `chmod 600` command and resulting permissions.
- [x] Screenshot showing the SHA-256 checksum.
- [x] Screenshot showing successful baseline verification.
- [x] Screenshot showing the sample file and baseline exist.

### 8. Conclusion

This exercise demonstrated fundamental Linux file security practices through access-permission management and SHA-256 integrity verification. These techniques provide a foundation for protecting files and detecting unexpected modifications during security operations.

**Phase status:** Practical commands completed according to the lab progress. Evidence screenshots and final documentation should be confirmed before submission.
