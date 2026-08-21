
# DB2 LUW 14-Day Bootcamp
# Day 1 – Foundations of DB2 LUW

> **Goal:** Build a strong conceptual understanding of DB2 LUW before touching installation and administration.

---

# Table of Contents

1. What is a Database Server?
2. DB2 Overview
3. DB2 LUW Architecture
4. Instance vs Database
5. DB2 Processes
6. Linux Basics for DB2 DBAs
7. Java/Spring Boot Analogies
8. Production Support Perspective
9. Common Interview Questions
10. Common Beginner Mistakes
11. Day 1 Cheat Sheet
12. Glossary

---

# 1. What is a Database Server?

A database is a collection of organized data.

A **database server** is software that manages that data by:
- Storing data
- Retrieving data
- Updating data
- Deleting data
- Handling concurrent users
- Providing security
- Recovering after crashes

Applications never access database files directly—they communicate with the database server using SQL.

Flow:

Application
↓
DB2 Server
↓
Database Files

---

# 2. DB2 Overview

DB2 is IBM's Relational Database Management System (RDBMS).

Major editions:
- DB2 for z/OS (IBM Mainframes)
- DB2 LUW (Linux, UNIX, Windows)

Typical enterprise users:
- Banking
- Insurance
- Government
- Healthcare
- Airlines

Your project uses **DB2 LUW on SUSE Linux running on AWS**.

---

# 3. DB2 LUW Architecture

Linux Server
↓
DB2 Instance
├── Memory
├── Processes
├── Configuration
└── Network Listener
↓
Database
↓
Tablespaces
↓
Physical Files

Main components:
- Client
- JDBC Driver
- DB2 Instance
- Database
- Tablespaces
- Buffer Pool
- Transaction Logs
- Disk Storage

---

# Buffer Pool

A Buffer Pool caches database pages in RAM.

Without Buffer Pool:
Application → Disk → Disk → Disk

With Buffer Pool:
Application → RAM → Disk (only when necessary)

Benefits:
- Faster queries
- Less disk I/O
- Better performance

---

# Transaction Logs

Every committed change is written to the transaction log before being permanently flushed to data files.

Purpose:
- Crash Recovery
- Rollback
- Backup consistency

---

# 4. Instance vs Database

## Instance

A running DB2 engine.

Contains:
- Processes
- Memory
- Connections
- Configuration

## Database

Persistent storage.

Contains:
- Tables
- Indexes
- Schemas
- Views
- Procedures
- Data

Relationship:

Instance
├── HRDB
├── SALESDB
└── TESTDB

One instance can host multiple databases.

Stopping the instance:
- Buffer Pool ❌ Lost
- Connections ❌ Lost
- Database ✅ Remains
- Transaction Logs ✅ Remain

---

# 5. Important DB2 Processes

## db2sysc
Main DB2 engine.

Responsibilities:
- Execute SQL
- Manage memory
- Coordinate DB2

## Logging
Writes transaction logs.

## Page Cleaner
Writes modified pages from RAM to disk.

## Prefetcher
Loads pages into RAM before they are requested.

## Lock Manager
Controls concurrent access.

## Deadlock Detector
Detects and resolves deadlocks.

Typical SQL flow:

Application
↓
db2sysc
↓
Lock Manager
↓
Buffer Pool
↓
Transaction Log
↓
Page Cleaner
↓
Disk

---

# 6. Linux Basics

Essential commands:

| Command | Purpose |
|---------|---------|
| pwd | Current directory |
| ls -la | List files |
| cd | Change directory |
| cat | Display file |
| tail -f | Monitor log |
| ps -ef \| grep db2 | DB2 processes |
| top | CPU/RAM |
| df -h | Disk usage |
| du -sh | Directory size |
| grep | Search text |
| find | Find files |
| whoami | Current user |

---

# 7. Java Analogies

| Java | DB2 |
|------|-----|
| JVM | DB2 Instance |
| Running Spring Boot | Running DB2 Engine |
| Java Heap | Buffer Pool |
| Object Cache | Cached Database Pages |
| PostgreSQL Database | DB2 Database |
| Threads | DB2 Processes |

---

# 8. Production Support Perspective

Typical investigation:

1. ps -ef | grep db2
2. df -h
3. top
4. tail -100 db2diag.log
5. Verify db2sysc
6. Check Buffer Pool
7. Check Transaction Logs

---

# 9. Interview Questions

1. What is DB2?
2. Difference between Instance and Database?
3. What is db2sysc?
4. Why are transaction logs important?
5. What is a Buffer Pool?
6. What happens during db2stop?
7. Can one instance host multiple databases?
8. Why does DB2 use multiple processes?

---

# 10. Common Beginner Mistakes

❌ Instance == Database

❌ Data lives in RAM

❌ Buffer Pool stores permanent data

❌ Logs are only for backups

Correct:
- Instance = Runtime engine
- Database = Persistent storage
- Buffer Pool = Cache
- Logs = Recovery mechanism

---

# 11. Day 1 Cheat Sheet

Remember:

- Database Server manages databases.
- DB2 is IBM's RDBMS.
- Instance = Engine.
- Database = Data.
- Buffer Pool = RAM cache.
- Transaction Logs = Crash recovery.
- db2sysc = Main DB2 process.
- Tablespaces store data physically.
- Linux is the operating environment.

---

# 12. Glossary

- DB2: IBM Relational Database Management System.
- LUW: Linux, UNIX and Windows.
- Instance: Running DB2 environment.
- Database: Persistent collection of data.
- Buffer Pool: Memory cache.
- Tablespace: Logical storage container.
- Transaction Log: Recovery log.
- db2sysc: Main DB2 process.
- Page Cleaner: Writes dirty pages to disk.
- Prefetcher: Reads pages into memory early.

---

# Revision Checklist

You should now be able to explain:

- Database vs Database Server
- DB2 LUW Architecture
- Instance vs Database
- Buffer Pool
- Transaction Logs
- db2sysc
- Linux commands for DB2 troubleshooting

Ready for Day 2: Installation, Instances, Databases, DB2 CLP, and Configuration.
