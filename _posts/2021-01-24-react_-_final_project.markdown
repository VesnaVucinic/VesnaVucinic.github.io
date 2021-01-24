---
layout: post
title:      "React - Final Project"
date:       2021-01-24 17:21:22 +0000
permalink:  react_-_final_project
---

In my project in React I implemented filter function to give possibility to user to filter images in search bar.
For that purpuse I set up state in class component AllBoards that shows group of images. After that I created const filteredBoards that uses filter method to return only images that matches user input in search bar. Finaly I used map method on filteredBoards to render on page all filtered images. You can see code below.
```
import React from 'react'
import { connect } from 'react-redux'
import { likeBoard } from '../actions/myBoards'
import { Card, Icon, Image, Label, Button, Input } from 'semantic-ui-react'

class AllBoards extends React.Component {
    state = {
        search: ""
    }

    handleChange = e => {
        this.setState({
            search: e.target.value
        })
    }

    render() {
        const { search } = this.state;
        const filteredBoards = this.props.boards.filter(board => {
            return board.attributes.name.toLowerCase().indexOf(search.toLowerCase()) !== -1})
        const allBoardsCards = this.props.boards.length > 0  
            ? 
            filteredBoards.map(board => (
                        <Card  key={board.id} style={{ width: '15rem'}}>
                            <Image src={board.attributes.image_url} wrapped ui={false}/>
                            <Card.Content>
                                <Card.Header>{board.attributes.name}</Card.Header>
                                <Card.Description>
                                    Uploaded by {board.attributes.user.name}
                                </Card.Description><br/>
                                {this.props.currentUser ?
                                    <Button as='div' labelPosition='right'>
                                        <Button icon  color='red' onClick={() => this.props.likeBoard(board)}>
                                            <Icon name='heart' />
                                            Like
                                        </Button>
                                        <Label as='a' basic color='red' basic pointing='left'>
                                            <strong>{board.attributes.likes}</strong>
                                        </Label>
                                    </Button>
                                : 
                                    <Button as='div' labelPosition='right'>
                                        <Button icon  color='red' >
                                            <Icon name='heart' />
                                            Liked
                                        </Button>
                                        <Label as='a'  color='red' basic pointing='left'>
                                            <strong>{board.attributes.likes}</strong>
                                        </Label>
                                    </Button>
                                }
                            
                            </Card.Content>
                        </Card>  
                    )) 
            : 
                null 

            return (
                <div>
                    {this.props.currentUser ?
                    <Input type='search' icon='search' placeholder='Search board' onChange={this.handleChange} size='large' style={{marginTop: '20px'}}/>
                    : null }
                    <Card.Group  style={{ margin: '15px', justifyContent: 'center'}}>
                        {allBoardsCards} 
                    </Card.Group>
                </div>
            )
    }
   
}


const mapStateToProps = state => {
    return {
        boards: state.allBoards,
        board: state.board,
        currentUser: state.currentUser
        
    }
}

export default connect(mapStateToProps, { likeBoard })(AllBoards)

```
