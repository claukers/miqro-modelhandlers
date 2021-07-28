# @miqro/modelhandlers

this module provides some transformation for sequelize calls and AuditHandler.


```typescript
import { parse } from "@miqro/core";
import { getWhereOptions, GROUP, ORDER, PAGINATION, GROUP } from "@miqro/modelhandlers";

const {limit, offset, group, q, columns} = parse("query", req.query, {
  ...ORDER(["createdAt", "id"]),
  ...GROUP(["status"]),
  ...SEARCH(["id"]),
  ...PAGINATION({
    defaultLimit: 10,
    maxlimit: 150
  })
} , "no_extra");
const {order} = req.query.order ? parseOrder(req.query.order) : undefined;

modelA.findAndCountAll({
  where: getWhereOptions({
    q, columns,
    filter: {
      ...
    }
  }),
  limit,
  offset,
  group,
  order
})
```

#### AuditHandler

```typescript
import { AuditHandler, AuditErrorHandler } from "@miqro/modelhandlers";

app.use(AuditHandler());
//app.use(AuditHandler("audit", sequelize, getLogger("AuditHandler")));
app.catch(AuditErrorHandler());
```
