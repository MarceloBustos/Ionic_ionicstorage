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
            <h1>Países Favoritos</h1>
            <ion-grid>
                <ion-row>
                    <ion-col size="12" size-md="6" size-lg="4">
                        <ion-select v-model="seleccionado" fill="outline" interface="action-sheet"
                            placeholder="Seleccione el país">
                            <ion-select-option v-for="(pais, i) in paises" :key="i" :value="pais">{{ pais
                                }}</ion-select-option>
                        </ion-select>

                        <ion-button fill="outline" expand="block" @click="agregar()">
                            Agregar a la lista
                        </ion-button>
                    </ion-col>
                </ion-row>
            </ion-grid>
            <template v-if="lista.length != 0">
                <h1>Lista de favoritos</h1>
                <!-- Invocar metodo eliminar lista para borra un elememento de la lista -->
                <ion-button color="danger" @click="eliminarLista">Borrar Lista</ion-button>
                <ion-list>
                    <ion-item v-for="(fav, i) in lista" :key="i">
                        <ion-label>{{ fav }}</ion-label>
                        <ion-button color="danger" @click="eliminarFavorito(i)">Borrar</ion-button>
                    </ion-item>
                </ion-list>
            </template>
        </ion-content>
    </ion-page>
</template>


<script>
import { IonContent, IonGrid, IonHeader, IonPage, IonRow, IonTitle, IonToolbar, IonCol, IonSelect, IonSelectOption, IonButton, IonList, IonItem, IonLabel } from '@ionic/vue';
import { } from 'ionicons/icons';

import { Storage } from '@ionic/storage';
import { DeprecationTypes } from 'vue';

export default {
    name: 'EjemploUno',
    components: {
        IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonGrid, IonRow, IonCol, IonSelect, IonSelectOption, IonButton, IonList, IonItem, IonLabel
    },
    data() {
        return {
            seleccionado: null,
            paises: ['Chile', 'España', 'Francia', 'Portugal', 'El Salvador'],
            //Variable para guardar los paises almacenados en el storage
            lista: [],

            //Variable para paises seleccionados
            favoritos: [],

            //Instancia de storage
            store: new Storage()
        }
    },
    methods: {
        async inicialStorage() {
            await this.store.create()
        },

        //Guardar datos en el storage
        async agregar() {
            if (this.seleccionado !== null) {
                this.favoritos.push(this.seleccionado)
                await this.store.set('paises', JSON.stringify(this.favoritos))
                this.seleccionado = null
                this.leer()
            }
        },
        async leer() {
            let datos = await this.store.get('paises')
            if (datos) {
                this.lista = JSON.parse(datos)
            }
            else {
                this.lista = []
            }
        },
        async eliminarLista() {
            await this.store.remove('paises')
            this.favoritos = []
            this.leer()
        },
        async eliminarFavorito(id) {
            this.favoritos.splice(id, 1)
            await this.store.set('paises', JSON.stringify(this.favoritos))
            this.leer()
        },
        ionViewWillEnter() {
            this.inicialStorage()
            this.leer()
        }
    }
}
</script>

<style></style>