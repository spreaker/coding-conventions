# Getter Template

```
#if($field.modifierStatic)
static ##
#end
$field.type ##
#set($cleanName = $StringUtil.replace($helper.getPropertyName($field, $project), "_", "", false))
#set($name = $StringUtil.capitalizeWithJavaBeanConvention($StringUtil.sanitizeJavaIdentifier($cleanName)))
#if ($field.boolean && $field.primitive)
  is##
#else
  get##
#end
${name}() {
  return this.$field.name;
}
```

# Setter Template

```
#set($paramName = $helper.getParamName($field, $project))
#set($cleanParamName = $StringUtil.replace($paramName, "_", "", false))
public ##
#if($field.modifierStatic)
static void ##
#else
  $classname ##
#end
#set($methodName = $StringUtil.sanitizeJavaIdentifier($helper.getPropertyName($field, $project)))
#set($cleanMethodName = $StringUtil.replace($methodName, "_", "", false))
set$StringUtil.capitalizeWithJavaBeanConvention($cleanMethodName)($field.type $cleanParamName) {
#if (!$field.modifierStatic)
this.##
#else
  $classname.##
#end
$field.name = $cleanParamName;
#if(!$field.modifierStatic)
return this;
#end
}
```
