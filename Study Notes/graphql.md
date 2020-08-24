


```yaml

{
    repository(owner: "github", name: "opensource.guide") {
        id
        name
        description
        watcher(first: 5) {
            edges {
                node {
                    id
                    name
                    company
                }
            }
        }
    }
    pullRequets(last: 4) {
        edges {
            node {
                id
                author {
                    avatarURL
                    login
                    path
                }
            }
        }
    }
}

# You can name your queries like this. Called operation name.
query FirstFiveOrgMembers {

}


# Using arguments variables

query FirstFiveOrgMembers($login: String!){ # ! means it's required.
    organization(login: $login) {
        id
        name
    }

}

# And then on QUERY VARIABLES:

{
    "login": "facebook" # or google, or airbnb, etc.
}


# MUTATIONS


mutation NewComment($input: AddCommentinput!) {
    addComment($input: $input) {
        clientMutationId
        subject {
            id
        }
    }
}

# And the QUERY VARIABLES:

{
    "input": {
        "clientMutationId": "515152",
        "subjectId", "thebase64id",
        "body": "Greate idea - thanks  you!"
    }
}


# Also

mutation NewReaction($input: AddReactionInput!) {
    addReaction(input: $input) {
        reaction {
            content
        }
    }
}

# And the QUERY VARIABLES:

{
    "input": {
        "clientMutationId": "465",
        subjectId: "theid",
        "content": "HOORAY"
    }
}


```