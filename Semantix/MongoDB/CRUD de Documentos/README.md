# CRUD de Documentos

1. Criar a collection teste no banco de dados seu nome

         db.createCollection('teste')
2. Inserir o seguinte documento:

- Campo: usuario, valor: Semantix
- Campo: data_acesso, valor: data atual no formato ISODate

        db.teste.insertOne({usuario: "Semantix", data_acesso: new Date()})
3. Buscar todos os documentos do ano >= 2020

        db.teste.find({data_acesso: {$gte: new Date("2020")}})
        
        -- ou com ISODate. No ISODate precisa informar uma data com formato completo
        db.teste.find({data_acesso: {$gte: ISODate("2020-01-01")}})
4. Atualizar o campo “data_acesso” para timestamp com o valor da atualização do usuario Semantix

        db.teste.updateOne({usuario: "Semantix"},{$currentDate: {data_acesso: {$type: "timestamp"}}})
5. Buscar todos os documentos

        db.teste.find()
6. Deletar o documento criado pelo id

        db.teste.deleteOne({_id: ObjectId("62a3204a154037b6547e328e")})
7. Deletar a collection

        db.teste.drop()
