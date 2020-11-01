# NoSQL

## Сущности

### point
id(Integer) - идентификатор точки из openstreetmap

lat(Float) - широта точки

lon(Float) - долгота точки

street(String) - название улицы

### road
nodes(Array) - список узлов ремонтируемой дороги


### plan
roads(Array) - список ремонтируемых дорог

# SQL

## Сущности

### point
id(Integer) - идентификатор точки из openstreetmap

lat(Float) - широта точки

lon(Float) - долгота точки

street(String) - название улицы

### road_section
id(Integer) - идентификатор участка дороги

### road_section_node
section_id(Integer) - идентификатор участка дороги

point_id(Integer) - идентификатор точки

### plan
id(Integer) - идентификатор плана

name(String) - название плана

### plan_road
plan_id - идентификатор плана

section_id - идентификатор участка дороги
