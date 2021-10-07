<template>
    <h1>Vee-Validateでフォームバリデーション</h1>

    <input type="text" v-model="name" />
    <p>{{ errors.name }}</p>

    <input type="email" :value="email" @blur="handleChange" />
    <p>{{ errors.email }}</p>
</template>

<script>
import { useField, useForm } from "vee-validate";
import { object, string } from "yup";

export default {
    setup() {
        const schema = object({
            name: string().required("必須の項目です。"),
            email: string()
                .required("必須の項目です。")
                .email("メールアドレスの形式ではありません。"),
        });

        const { errors } = useForm({
            validationSchema: schema,
        });

        const { value: name } = useField("name");
        const { value: email, handleChange } = useField("email");

        console.log({ value: email, handleChange });

        return {
            name,
            email,
            errors,
            handleChange,
        };
    },
};
</script>
