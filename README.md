# MQTT S.IoT - Documentação

Para publicar via MQTT é necessário ter os dados como o modelo de configuração abaixo.
* Para 'username' utilize o ID da máquina cadastro no SIOT.
* Para 'password' utilize o token de integração da máquina gerado no SIOT.

```
host: mqtts://test-mqtt.siot.konztec.com:8883
username: iot
password: geeM/H1MvkyaYFcC/hT47w==
```


### <strong>Payload Simples</strong>

Poderá ser enviado um valor simples no payload como abaixo:

<strong>Topic</strong>
```
/siot/{maquina_id}/{sensor_id}/{signal_id}
```
<strong>Payload</strong>
```
{value}
```

Onde os parâmetros `{maquina_id}`, `{sensor_id}`, `{signal_id}` são de acordo com o cadastrado no portal S.IoT.
E `{value}` e o valor do sinal.

##### <strong>Exemplo</strong>:

```
topic: /siot/iot_temperature/temperature/atual
payload: 17
```

<br/>

### <strong>Payload JSON</strong>

Poderá ser enviado um JSON contendo vários sensores no payload:

<strong>Topic</strong>
```
/siot/s/{maquina_id}
```
<strong>Payload</strong>
```
{
    "idMachine": "{maquina_id}",
    "date": "{date_dispositivo}",
    "sensors": [
        {
            "sensorId": "{sensor_id}",
            "status": "{status_sensor}",
            "signals": [
                {
                    "signal": "{signal_id}",
                    "value": "{value}"
                }
            ]
        }
    ]
  
}
```

Onde os parâmetros `{maquina_id}`, `{sensor_id}`, `{signal_id}` são de acordo com o cadastrado no portal S.IoT.
`{status_sensor}` o estado atual do sensor sendo possível enviar uma das opções a frente: <strong>'`active`','`active`','`problem`'</strong>. E a `{data_dispositivo}` data/hora do dispositivo e o `{value}` valor do sinal.

##### <strong>Exemplo</strong>:

```
topic: /siot/s/iot_2
payload: {
    "idMachine": "iot_2",
    "date": "2020-03-20T12:05:20.000Z",
    "sensors": [
        {
            "sensorId": "battery",
            "status": "active",
            "signals": [
                {
                    "signal": "percentual",
                    "value": 75
                },
                {
                    "signal": "tension",
                    "value": 25.5,
                    "unity": "V"
                }
            ]
        },
        {
            "sensorId": "temperature",
            "status": "lostconnection",
            "signals": [
                {
                    "signal": "atual",
                    "value": 23
                }
            ]
        }
    ]
  
}
```