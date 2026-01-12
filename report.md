
```bash
[Title]
Pbrong/hrms has a Stored Cross Site Scripting vulnerability

[PRODUCT]
[hrms1.0.1](https://github.com/pbrong/hrms/releases/tag/1.0.1)

[TYPE]
Stored Cross Site Scripting Vulnerability

[DESCRIPTION]
Pbrong/hrms has a Stored Cross Site Scripting vulnerability. This vulnerability is due to the fact that the UpdateRecruitmentById function under hrms1.0.1/handler/recruitment.go does not filter the parameters passed by the user, resulting in the system being able to parse javascript and S Tored Cross Site Scripting vulnerability.

ANALYZE：

Find any place where you can fill in the information, such as: recruitment information-related `recruitment`, first obtain the data and then enter it to `UpdateRecruitmentById`:

```

[![image-20250226130453888](image-20250226130453888.png)

![image-20250226130511486](./img_%E6%8F%90%E4%BA%A4cve/image-20250226130511486.png)

Then deposit it into `service.UpdateRecruitmentById`, and then put it into the database:

![image-20250226130647961](./img_%E6%8F%90%E4%BA%A4cve/image-20250226130647961.png)

If it is displayed, enter the `query` route:

![image-20250226130742463](./img_%E6%8F%90%E4%BA%A4cve/image-20250226130742463.png)

Enter the `GetRecruitmentByJobName` method:

![image-20250226130815279](./img_%E6%8F%90%E4%BA%A4cve/image-20250226130815279.png)

Get data through `service.GetRecruitmentByJobName`:

![image-20250226130901031](./img_%E6%8F%90%E4%BA%A4cve/image-20250226130901031.png)

During this period, no `xss` filtering was done, resulting in the existence of storage-type `xss` vulnerabilities.

POC：

Enter the recruitment management function:

![image-20250226131011222](./img_%E6%8F%90%E4%BA%A4cve/image-20250226131011222.png)

![image-20250226131029355](./img_%E6%8F%90%E4%BA%A4cve/image-20250226131029355.png)
