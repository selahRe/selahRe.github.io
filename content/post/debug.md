```kotlin
fun existsBySnAndDate(inverterSn: String, date: Int): Boolean{
            val result = Core.Q().queryByCols(InverterPacDay::class.java, mapOf("inverter_sn" to inverterSn, "date" to date))
            print("result空 $result.isNullOrEmpty()")
            return !result.isNullOrEmpty()
        }
        
 public <T extends BaseModel> List<T> queryByCols(Class<T> c, Map<String, Object> kvs) {
        return this.<T>processQueryResultMaps(c, this.queryRawByCols(c, kvs));
    }
    
 public <T extends BaseModel> List<Map<String, Object>> queryRawByCols(Class<T> c, Map<String, Object> kvs) {
        CoreModel.shared().ensureModelClass(c);
        if (kvs != null && kvs.size() != 0) {
            Collection<Condition> conditions = new ArrayList();

            for(String key : kvs.keySet()) {
                Object value = kvs.get(key);
                conditions.add(DSL.field(key).eq(value));
            }

            return this.queryRawByCols(c, conditions);
        } else {
            return null;
        }
    }
    
    public <T extends BaseModel> List<Map<String, Object>> queryRawByCols(Class<T> c, Object... args) {
        CoreModel.shared().ensureModelClass(c);
        if (args.length != 0 && args.length % 2 == 0) {
            List<Condition> conditionList = new ArrayList();

            for(int i = 0; i < args.length / 2; ++i) {
                if (!(args[i * 2] instanceof String)) {
                    return null;
                }

                String colName = (String)args[i * 2];
                Object colValue = args[i * 2 + 1];
                conditionList.add(DSL.field(colName).eq(colValue));
            }

            return this.queryRawByCols(c, conditionList);
        } else {
            return null;
        }
    }
    
     public <T extends BaseModel> List<Map<String, Object>> queryRawByCols(Class<T> c, List<Condition> conditions) {
        CoreModel.shared().ensureModelClass(c);
        if (conditions != null && conditions.size() != 0) {
            DSLContext dsl = this.getDSLContext();
            Model model = CoreModel.shared().getModel(c);
            if (model.enableWeight()) {
                conditions.add(DSL.field("weight").greaterOrEqual(0));
            }

            JdbcTemplate jdbcTemplate = this.getJdbcTemplate();
            Query query = dsl.select(new SelectFieldOrAsterisk[0]).from(DSL.name(model.tableName())).where(conditions);
            List<Map<String, Object>> resultMapList = jdbcTemplate.queryForList(query.getSQL(), query.getBindValues().toArray());
            return resultMapList.size() == 0 ? null : resultMapList;
        } else {
            return null;
        }
    }
    
```