# NoSQL

## Сущности
### point 
id(Integer) - идентификатор точки из openstreetmap

lat(Float) - широта точки

lon(Float) - долгота точки

street(String) - название улицы

### road_section
id(Integer) - идентификатор секции

points_ids(Array) - идентификаторы точек, принадлежащих секции

### plan
id(Integer) - идентификатор плана ремонта

roads(Array) - идентификаторы дорог, принадлежащих плану

# SQL

## Таблицы

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

## Размер данных

Vpoint = Vid + Vlon + Vlat = 8B + 4B + 4B + 32B = 48B

Vroad_section = Vid = 8B

Vroad_section_node = Vsection_id + Vpoint_id = 8B + 8B = 16B

Vplan = Vid + Vname = 8B + 16B = 24B

Vplan_road = Vplan_id + Vsection_id = 8B + 8B = 16B

V = 
