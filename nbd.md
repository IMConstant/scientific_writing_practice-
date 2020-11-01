# NoSQL

## Сущности
### point 
id(Integer) - идентификатор точки из openstreetmap

lat(Float) - широта точки

lon(Float) - долгота точки

street(String) - название улицы

### relations
id(Integer) - идентификатор отношения

points_ids(Integer) - идентификаторы соседних точек

### road_section
id(Integer) - идентификатор секции

lat(Float) - широта начальной точки

lon(Float) - широта конечной точки

points_ids(Array) - идентификаторы точек, принадлежащих секции

### plan
id(Integer) - идентификатор плана ремонта

roads(Array) - идентификаторы дорог, принадлежащих плану

## Размер данных
Vpoint = Vid + Vlon + Vlat + Vstree = 8B + 4B + 4B + 32B = 48B

Vrelations = Vid + Vpoints_ids(~3) = 8B + 3 * 8B = 32B

Размер участка дороги сильно зависит от количества точек, принадлежащих ей, поэтому возьмем среднее значение в 3 точки.

arr_length = 3

Vroad_section = Vid + Vpoints_ids + Vlat + Vlon = 8B + 4B + 4B + arr_length * 8B = 48B

Пример среднее количество участков дороги в одном плане равным 2

Vplan = Vid + Vroads_ids = 8B + 2 * 8B = 24B

V1 = Vroad_section + Vplan = 48B + 24B = 72B

V2 * Vpoint + Vrelations = 48B + 32B = 80B

V = V2 + V1 = 72B + 80B = 152B

Размер используемой памяти зависит от количества планов и количества узлов, слeдовательно

Vp(N) = N * V1 = N * 72B - объем памяти для плановых работ, где N - количество планов ремонтных работ

Vg(N) = N * V2 = N * 80B - обхем памяти хранимых узлов и отношений, где N - количество хранимых узлов


# SQL

## Таблицы

### point
id(Integer) - идентификатор точки из openstreetmap

lat(Float) - широта точки

lon(Float) - долгота точки

street(String) - название улицы

### relations
p1_id(Integer) - идентификатор первого узла
p2_id(Integer) - идентификатор второго узла

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

Vpoint = Vid + Vlon + Vlat + Vstreet = 8B + 4B + 4B + 32B = 48B

Vrelations = Vp1_id + Vp2_id = 8B + 8B = 16B

Vroad_section = Vid = 8B

Vroad_section_node = (~3) * (Vsection_id + Vpoint_id) = 3 * (8B + 8B) = 48B

Vplan = Vid + Vname = 8B + 16B = 24B

Vplan_road = Vplan_id + (~3) * Vsection_id = 8B + 3 * 8B = 32B

V1(Объем данных плановых работ) = Vroad_section + Vroad_section_node + Vplan + Vplan_road = 8B + 48B + 24B + 32B = 112B

V2(Обхем данных хранимых узлов и отношений) = Vpoint + (~3) * Vrelations = 48B + 3 * 16B = 96B

V = V1 + V2 = 112B + 96B = 208B

Vp(N) = N * V1 = N * 112B - объем памяти для плановых работ, где N - количество планов ремонтных работ

Vg(N) = N * V2 = N * 96B - обхем памяти хранимых узлов и отношений, где N - количество хранимых узлов
