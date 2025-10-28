# Module 2: First Deployment - Building Your Foundation


## 🎯 Module Objectives

In this module, you'll deploy your first complete data engineering solution to Microsoft Fabric:

✅ Deploy a medallion architecture (Bronze → Silver)  
✅ Create and populate Lakehouses with sample data  
✅ Set up data transformation notebooks  
✅ Configure a semantic model and Power BI report  
✅ Validate the end-to-end data flow

## 📝 Exercise 1: Authenticate Fabric CLI (3 minutes)

> **Goal:** Connect fabric-cli to your Microsoft Fabric account.
>
> [!NOTE]
> This is a one-time setup that persists across sessions.

```bash
# Authenticate with Fabric
fab auth login
```

**What happens:**
1. Browser opens to Microsoft login
2. Sign in with workshop credentials
3. Grant permissions to fabric-cli
4. Return to terminal when complete

**Verify authentication:**
```bash
fab auth status
```

Should list account, tenant id and other information.

## 📝 Exercise 2: Run Bootstrap Deployment (10 minutes)

> **Goal:** Deploy the complete data engineering solution to your workspace.

### Step 2.1: Navigate to Deployment Directory

```bash
# From the workshop root directory
cd deployment/

# Verify you're in the right place
ls
# You should see: first_deployment.sh, bootstrap.md, etc.
```

### Step 2.2: Execute the Deployment Script

> [!IMPORTANT]
> Replace ```yourusername``` with the name provided by your instructor. Remove the `CICD.` prefix. No email suffix. Lowercase.
> For example: If your user is: **`CICD.user020`**, use **`user020`**
> Replace "Your-Capacity-Name" with the actual capacity name provided by your instructor. 

**For Windows (WSL)/macOS/Linux:**
```bash
./first_deployment.sh \
    --username yourusername \
    --capacity-name "Your-Capacity-Name"
```

> [!TIP]
> **Confirming Your Capacity Name:**
> 1. Go to Fabric portal
> 2. Click Settings (⚙️) → Admin portal
> 3. Select "Capacities"
> 4. Copy the exact capacity name

### Step 3: Monitor the Deployment Progress

> [!NOTE]
> This process takes 5-10 minutes. Each step will show progress indicators.

**What the script does:**

| Stage | Action | Duration |
|-------|--------|----------|
| 1️⃣ | Create workspace `DEWorkshop_<username>` | ~30 sec |
| 2️⃣ | Assign to Fabric capacity | ~10 sec |
| 3️⃣ | Create Bronze & Silver Lakehouses | ~1 min |
| 4️⃣ | Import notebooks and artifacts | ~2 min |
| 5️⃣ | Configure data connections | ~1 min |
| 6️⃣ | Load sample data | ~2 min |
| 7️⃣ | Open workspace in browser | Instant |

### Step 4: Watch for Success Messages

**Expected output:**
```text
_ creating staging directory...
* Done

_ creating a workspace...
...

_ assigning capacity...
...

_ creating lakehouses...
Creating a new Lakehouse...
* 'Lakehouse_Bronze.Lakehouse' created
Creating a new Lakehouse...
* 'Lakehouse_Silver.Lakehouse' created

_ importing an environment...
Importing './tmp/MyEnv.Environment' → '/DEWorkshop_yourusername.Workspace/MyEnv.Environment'...
* Updated Spark Settings
* Published
* 'MyEnv.Environment' imported

_ getting items metadata...
  - Workspace ID: cbf21339-2d31-4f00-b6bd-2751c5ec2e84
  - Lakehouse Bronze ID: 025370db-d6cf-4dd5-b4dd-c97db285e4a2
  - Lakehouse Silver ID: 0b56b1e2-e931-495d-8bce-dc44178c9327
  - Lakehouse Silver SQL Endpoint ID: a6048652-3afc-4fad-ad90-af7d38c506ff
  - Lakehouse Silver SQL Endpoint Conn String: x6eps4xrq2xudenlfv6naeo3i4-hej7fszrfuae7nv5e5i4l3boqq.msit-datawarehouse.fabric.microsoft.com
* Done

_ importing a notebook...
Importing './tmp/Bronze_Data_Preparation.Notebook' → '/DEWorkshop_yourusername.Workspace/Bronze_Data_Preparation.Notebook'...
* 'Bronze_Data_Preparation.Notebook' imported
! Modifying properties may lead to unintended consequences
Setting new property for 'Bronze_Data_Preparation.Notebook'...
* Item updated

_ importing a notebook...
Importing './tmp/Transformations.Notebook' → '/DEWorkshop_yourusername.Workspace/Transformations.Notebook'...
* 'Transformations.Notebook' imported
! Modifying properties may lead to unintended consequences
Setting new property for 'Transformations.Notebook'...
* Item updated

_ importing a notebook...
Importing './tmp/Validations.Notebook' → '/DEWorkshop_yourusername.Workspace/Validations.Notebook'...
* 'Validations.Notebook' imported
! Modifying properties may lead to unintended consequences
Setting new property for 'Validations.Notebook'...
* Item updated
! Modifying properties may lead to unintended consequences
Setting new property for 'Bronze_Data_Preparation.Notebook'...
* Item updated

_ importing a copy job...
Importing './tmp/MyLHCopyJob.CopyJob' → '/DEWorkshop_yourusername.Workspace/MyLHCopyJob.CopyJob'...
* 'MyLHCopyJob.CopyJob' imported

_ importing a copy job...
Importing './tmp/MyLHCopyJob2.CopyJob' → '/DEWorkshop_yourusername.Workspace/MyLHCopyJob2.CopyJob'...
* 'MyLHCopyJob2.CopyJob' imported

_ running a copy job...
CopyJob started. Waiting for completion...

_ running a copy job...
CopyJob started. Waiting for completion...
* CopyJob executions finished

_ creating t2 shortcut to silver lakehouse...
Creating a new Shortcut...
* 't2.Shortcut' created

_ running notebook...
Running job (sync) for 'Bronze_Data_Preparation.Notebook'...
∟ Job instance 'c0c3ac83-5db5-4d17-9eca-36f75fd6e1b3' created
∟ Timeout: no timeout specified
∟ Job instance status: NotStarted
...
∟ Job instance status: InProgress
∟ Job instance status: Completed
* Job instance 'c0c3ac83-5db5-4d17-9eca-36f75fd6e1b3' Completed

_ creating t3 shortcut to silver lakehouse...
Creating a new Shortcut...
* 't3.Shortcut' created

_ running notebook...
Running job (sync) for 'Transformations.Notebook'...
∟ Job instance '5167928c-a393-4fbf-a8f0-696f69bf50a1' created
∟ Timeout: no timeout specified
∟ Job instance status: NotStarted
...
∟ Job instance status: NotStarted
∟ Job instance status: Completed
* Job instance '5167928c-a393-4fbf-a8f0-696f69bf50a1' Completed

_ importing a semantic model...
Importing './tmp/MySemanticModel.SemanticModel' → '/DEWorkshop_yourusername.Workspace/MySemanticModel.SemanticModel'...
* 'MySemanticModel.SemanticModel' imported

_ importing a powerbi report...
Importing './tmp/MyReport.Report' → '/DEWorkshop_yourusername.Workspace/MyReport.Report'...
* 'MyReport.Report' imported

_ opening workspace...
Opening 'DEWorkshop_yourusername.Workspace' in the web browser...
* https://app.powerbi.com/groups/cbf21339-2d31-4f00-b6bd-2751c5ec2e84/list?experience=fabric-developer

_ cleaning up staging directory...
* Done
```

> [!SUCCESS]
> If you see "Deployment complete!", you're ready to validate!

## 📝 Exercise 3: Verify Workspace Contents (5 minutes)

> **Goal:** Confirm all artifacts were created successfully in your workspace.

### Step 3.1: Check Workspace Items

**In the Fabric portal, your workspace should show:**

| Item | Type | Status Check |
|------|------|-------------|
| Lakehouse_Bronze | 🏠 Lakehouse | Should contain 4 tables |
| Lakehouse_Silver | 🏠 Lakehouse | Should contain 3 tables |
| MyLHCopyJob | 📥 Copy Activity | Status: Completed |
| MyLHCopyJob2 | 📥 Copy Activity | Status: Completed |
| Bronze_Data_Preparation | 📓 Notebook | Ready to run |
| Transformations | 📓 Notebook | Ready to run |
| Validations | 📓 Notebook | Ready to run |
| MyEnv | Environment |  |
| MySemanticModel | 📊 Semantic Model | Connected to Silver (refresh it!) |
| MyReport | 📈 Report | Should open without errors (refresh it!) |


## 📝 Exercise 4: Validate Data in Lakehouses (5 minutes)

> **Goal:** Verify that data was successfully loaded into your Lakehouses.

> [!NOTE]
> The **Validations** notebook contains automated checks for all data quality and table counts.

1. **Open the Validations notebook:**
    - Click on **Validations** in your workspace
    - The notebook will open in edit mode

2. **Execute the validation checks:**
    - Make sure MyEnv is selected as the environment
    - Click **Run all** button at the top
    - Wait for all cells to complete (approximately 1-2 minutes)
    - Verify the table counts. The created shortcut to t3 should point to t3_dev in Bronze Lakehouse.
## 📝 Exercise 5: Test Complete Solution (7 minutes)

> **Goal:** Validate the end-to-end solution including transformations and reporting.

### Step 5.1: Run Data Quality Checks

> [!TIP]
> This helps you understand the data flow and validates transformations

1. Open **Validations** notebook
2. Click **Run all** button
3. Review output showing:
   - Row counts for each table
   - Data quality metrics
   - Schema validations
4. All checks should pass ✅

### Step 5.2: Test Semantic Model and Report

#### 📊 Verify Semantic Model:
1. Open **MySemanticModel**
2. Check data source connection:
   - Should point to `Lakehouse_Silver`
   - Table `dbo.t1` should be imported
3. Click **Refresh now** to update data

#### 📈 Open the Report:
1. Click on **MyReport**
2. Report should display:
   - Dashboard with charts
   - Interactive filters
   - No error messages
3. Try interacting with filters to ensure responsiveness

> [!SUCCESS]
> **Congratulations!** You've deployed your first Fabric solution! 🎉

> **[→ Click here to start Module 3: Version Control Basics](../versioning/start.md)**
