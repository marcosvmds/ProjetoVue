<template>
    <div class="adminPages">
        <PageTitle icon="fa fa-cogs" main="Administração do Sistema"
            sub="Cadastros & cia" />
            <div class="admin-pages-tabs">
                <b-card no-body>
                    <b-tabs>
                        <b-tab title="Artigos" active>
                            <ArticleAdmin/>
                        </b-tab>
                         <b-tab title="Categorias" active>
                            <CategoryAdmin/>
                        </b-tab>
                         <b-tab title="Usuários" active>
                            <UserAdmin/>
                        </b-tab>
                    </b-tabs>
                </b-card>
            </div>
    </div>
  
</template>

<script>
import PageTitle from '@/components/templates/PageTitle'
import ArticleAdmin from './ArticleAdmin'
import CategoryAdmin from './CategoryAdmin'
import UserAdmin from './UserAdmin'

export default {
    name: 'AdminPages',
    components: {PageTitle, ArticleAdmin, CategoryAdmin, UserAdmin}
}
</script>

<style>

	h1{
		font-size: 2rem;
	}
	h2{
		font-size: 1.5rem;
	}

    
</style>