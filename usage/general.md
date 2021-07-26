# Getting Started

We have **two** types of endpoints right now. Old-async one, based on `/webapi/Transaction2/SubmitTransaction` and `/webapi/Transaction2/GetTransactionResult`, and new-sync one - based on the `/api/process` method, which returns results in the **same** HTTP call. They are **not** connected, thus you can **not** use transaction id from the process to get results in GetTransactionResult. Basically, the **old** one is **deprecated**, and we **suggest** all our **new** customers use a new one.

{% hint style="info" %}
New version of Regula Document Reader Web Service **supports** requests from the old **Transaction** API.  
That means if you run a **new** web service and send a **Transaction** request following the old logic, you will get the result processed using new logic but in the format of the old web service interface.

To switch to a **new** api see [migration guide](general.md#migration-from-old-transactional-api)
{% endhint %}

## Migration From Old Transactional API

Steps for the migration: 

1. Uninstall old Regula Document Reader Web Service   
2. [Install](../installation/general.md) a new Regula Document Reader Web Service   
3. Rename license file `SLXXXXX` to `regula.license`. Place it according to **setup license** sections of [your platform installation guide](../installation/platforms/)   
4. \[Optional\] If you plan to migrate from **Windows**, ask your sales manager for a new license  
5. Run a new Regula Document Reader Web Service

