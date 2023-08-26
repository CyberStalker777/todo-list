<template>
    <Transition name="modal">
        <div class="modal" @click="closeModal">
            <div class="modal__block" @click.stop="">

                <h3 class="modal__block_title">{{ edit ? 'Изменить заметку' : 'Добавить заметку' }}</h3>

                <div class="modal__block_inputs">
                    <label>
                        <span class="modal__block_inputs-span" id="error1">Title</span>
                        <input v-model="title" type="text" placeholder="Введите название заметки">
                    </label>

                    <label>
                        <span class="modal__block_inputs-span" id="error2">Content</span>
                        <textarea v-model="text" wrap="off" placeholder="Введите текст заметки"></textarea>
                    </label>
                </div>

                <div class="modal__block_btns">
                    <button class="modal__block_btns-btn del" @click="closeModal">Отмена</button>
                    <button v-if="!edit" class="modal__block_btns-btn edit" @click="addNote">Добавить</button>

                    <button v-else class="modal__block_btns-btn edit" @click="changeNote">Изменить</button>
                </div>

            </div>
        </div>
    </Transition>
</template>

<script>

import { v4 as uuidv4 } from 'uuid';

export default {
    props: {
        edit: {
            typeof: Boolean
        },
        editedNote: {
            typeof: Object
        }
    },
    data() {
        return {
            title: '',
            text: '',
        }
    },
    methods: {
        closeModal() {
            this.$emit('close')
            this.title = this.text = ''
        },
        addNote() {
            if (this.title == '') {
                    let error1 = document.getElementById("error1");
                    
                        error1.classList.remove("modal__block_inputs-span");
                        error1.classList.add("error");
                }else{       
                    error1.classList.remove("error");
                    error1.classList.add("modal__block_inputs-span");
                }
            
                if (this.text == '') {
                    let error2 = document.getElementById("error2");
                    
                    error2.classList.remove("modal__block_inputs-span");
                    error2.classList.add("error");
                }else{
                    error2.classList.remove("error");
                    error2.classList.add("modal__block_inputs-span");
                }    
            
            if (this.title != '' && this.text != '') {
                const note = {
                    id: uuidv4(),
                    title: this.title,
                    text: this.text,
                    // 19.04.2023
                    date: new Date().toLocaleDateString()
                }
                this.$emit('addNote', note)
                this.closeModal()
            }

        },
        changeNote() {
            let newEditNote = {
                id: this.editedNote.id,
                title: this.title,
                text: this.text,
                date: new Date().toLocaleDateString()
            }
            this.$emit('changedNote', newEditNote)
            this.closeModal()
        }
    }
}
</script>


