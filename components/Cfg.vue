<template>
    <h1>{{ op }}</h1>
    <h2>Grammar Info</h2>
    <table>
        <tbody>
            <tr>
                <td>After</td>
                <td>{{ op }}</td>
            </tr>
            <tr>
                <td>Num syms</td>
                <td>{{ content.sym_source.next_symbol.n - 1 }}</td>
            </tr>
            <tr>
                <td>Num rules</td>
                <td>{{ content.rules.length }}</td>
            </tr>
        </tbody>
    </table>
    <h2>Rules</h2>
    <table>
        <thead>
            <th>LHS</th>
            <th>RHS</th>
        </thead>
        <tbody>
            <tr v-for="rule in content.rules">
                <td>{{ name_of(rule.lhs) }}</td>
                <td>
                    <span v-for="sym in rule.rhs">
                        {{ name_of(sym) }},
                    </span>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: ['op', 'content'],
    methods: {
        name_of(sym) {
            let name = this.content.sym_source.names[sym.n - 1]
            if (name === undefined || name == null) {
                return `g(${sym.n - 1})`
            } else {
                return `${name.name} (${sym.n - 1})`
            } 
        },
    }
}

</script>
