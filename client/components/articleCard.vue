<template>
    <div class="card margin-m flex flex-column justify-content-space-between">
        <div class="media media-1 spinner">
            <img v-bind:src="image" />
        </div>
        <div>
            <div class="flex flex-row justify-content-space-between">
                <p class="padding-left-m padding-top-s padding-right-s lead">{{title}}</p>
                <button v-on:click="showDeleteModal" class="button button-xxs button-gray button-border margin-top-s margin-right-m"><i class="fas fa-trash"></i></button>
            </div>
            <p class="padding-left-m padding-bottom-m padding-right-m" v-html="description"></p>
        </div>
        <div class="margin-right-2 button-group button-group-block">
            <button v-on:click="$emit('clicked-form', index)" class="button button-s button-primary">Manage</button>
            <button v-on:click="$emit('clicked-detail', index)" class="button button-s button-war">View</button>
        </div>
    </div>
</template>

<script>
    export default {
        methods: {
            showDeleteModal() {
                let self = this
                this.$modal.show('dialog', {
                    title: 'Yakin mau hapus yang ini?!',
                    text: 'Artikel dengan judul: ' + self.title,
                    buttons: [
                        {
                            title: 'Ya!',
                            handler: () => { 
                                self.$emit('delete-article', self.index)
                                this.$modal.hide('dialog')
                            }
                        },
                        {
                            title: 'Eh kepencet!',       // Button title
                        },
                    ]
                })
            }
        },
        props: ['title', 'description', 'image', 'index'],
    }
</script>