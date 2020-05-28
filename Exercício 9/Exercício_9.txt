//NOME: Mateus Agostinho dos Anjos
//NUSP: 9298191

//Consulta a)

db.equipamentos.find(
    {$and: [{preco: {$gte: 200, $lte: 300}}, {tipo: 'impressora'}]}, 
    {_id: 0, modelo: 1, tipo: 1, preco: 1}
);

//Consulta b)

db.equipamentos.find(
    {$or: [{tipo: 'impressora'}, {tipo: 'pc'}]},
    {_id: 0, fabricante: 1}
);

//Consulta c)

db.equipamentos.find(
    {$and: [{$or: [{cd: '6x'}, {cd: '8x'}]}, {preco: {$lte: 2000}}]},
    {_id: 0, modelo: 1, velocidade: 1, hd: 1},
).sort({velocidade: -1, tamanho: -1});

//Consulta d)

db.equipamentos.find(
    {fabricante: {$regex: '^[a, b, c, d, e]+', $options: 'i'}},
    {_id: 0, modelo: 1},
).sort({fabricante: 1});

db.fabricantes.find(
    {fabricante: {$regex: '^[a, b, c, d, e]+', $options: 'i'}},
    {_id: 0, 'equipamentos.modelo': 1},
).sort({fabricante: 1});

//Consulta e)

db.equipamentos.distinct(
    "tipo",
    {fabricante: {$regex: '[a-z0-9]+ [a-z0-9]+ [a-z0-9]+[ a-z0-9 ]*', $options: 'i'}},
    {_id: 0, fabricante: 1, tipo: 1},
);

db.fabricantes.distinct(
    "equipamentos.tipo",
    {fabricante: {$regex: '[a-z0-9]+ [a-z0-9]+ [a-z0-9]+[ a-z0-9 ]*', $options: 'i'}},
    {_id: 0, "equipamentos.tipo": 1},
);

//Consulta f)

db.equipamentos.distinct(
    "tipo",
    {fabricante: {$regex: '^[a-z0-9]+ [a-z0-9]+$', $options: 'i'}},
    {_id: 0, fabricante: 1, tipo: 1},
);

db.fabricantes.distinct(
    "equipamentos.tipo",
    {fabricante: {$regex: '^[a-z0-9]+ [a-z0-9]+$', $options: 'i'}},
    {_id: 0, "equipamentos.tipo": 1},
);

//Consulta g)
//Existem impressoras que nao possuem o campo "tipo_impressao", portanto
//as considerei como não coloridas

db.equipamentos.find(
    {$and: [{tipo: 'impressora', colorida: 1, tipo_impressao: {$ne: 'ink-jet'}}]},
    {_id: 0, fabricante: 1, modelo: 1}
);

//Consulta h)

db.equipamentos.find(
    {},
    {_id: 0, fabricante: 1, modelo: 1, preco: 1}
);

db.fabricantes.find(
    {},
    {_id: 0, fabricante: 1, 'equipamentos.modelo': 1, 'equipamentos.preco': 1}
);

