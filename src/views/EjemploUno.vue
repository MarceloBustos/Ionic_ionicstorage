<template>
    <ion-page>
        <ion-header>
            <ion-toolbar color="primary">
                <ion-title>
                    Ionic Storage
                </ion-title>
            </ion-toolbar>
        </ion-header>

        <ion-content class="ion-padding">
            <h1>Promedio</h1>
            <ion-grid>
                <ion-row>
                    <ion-col>
                        <ion-input fill="outline" label="30%" placeholder="Nota 1" v-model="nota1"
                            type="number"></ion-input>
                    </ion-col>
                </ion-row>

                <ion-row>
                    <ion-col>
                        <ion-input fill="outline" label="70%" placeholder="Nota 2" v-model="nota2"
                            type="number"></ion-input>
                    </ion-col>
                </ion-row>

                <ion-row v-show="(nota1 > 0 && nota2 > 0)">
                    <ion-col>
                        <ion-button @click="calcularPromedio()" fill="outline" expand="block" color="success">Calcular
                            Promedio</ion-button>
                    </ion-col>
                </ion-row>
            </ion-grid>

            <ion-alert :is-open="alertState" header="Respuesta" :message="alertMessage"
                @didDismiss="alertState = false"></ion-alert>
        </ion-content>
    </ion-page>
</template>

<script>
import { IonContent, IonGrid, IonHeader, IonPage, IonTitle, IonToolbar, IonRow, IonCol, IonInput, IonButton, IonAlert } from '@ionic/vue';
import { } from 'ionicons/icons';
import { Storage } from '@ionic/storage';

export default {
    name: 'EjemploUno',
    components: {
        IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol, IonInput, IonButton, IonAlert
    },
    data() {

        return {
            //Variables para capturar las notas de los IonInputs
            nota1: 0,
            nota2: 0,

            //Variable para controlar la visibilidad del IonAlert
            alertState: false,

            //Variable para guardar el mensaje de los IonAlerts
            alertMessage: ''
        }
    },
    methods: {
        async calcularPromedio() {
            //Iniciar el storange
            let storage = new Storage()

            //crear storage
            await storage.create()

            //Guardar notas en el storage
            await storage.set('nota1', this.nota1)
            await storage.set('nota2', this.nota2)

            //Obtener notas del Storage
            let n1 = await storage.get('nota1')
            let n2 = await storage.get('nota2')

            //Calcular promedio
            this.alertMessage = 'Su promedio es: ' + ((n1 * 0.3) + (n2 * 0.7)).toFixed(2)

            //Mostrar alerta
            this.alertState = true
        }
    }
}
</script>

<style></style>