# Students
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;
using System.Drawing;
using Color = Microsoft.Xna.Framework.Color;


namespace pongg
{
    public class Game1 : Game
    {
        Texture2D ballTexture;

        private GraphicsDeviceManager _graphics;
        private SpriteBatch _spriteBatch;
        Vector2 ballPosition;
        float ballSpeed;

        public Game1()
        {
            _graphics = new GraphicsDeviceManager(this);
            Content.RootDirectory = "Content";
        }

        protected override void Initialize()
        {
            // TODO: Add your initialization logic here

            base.Initialize();
            ballPosition = new Vector2(_graphics.PreferredBackBufferWidth / 2,
                                 _graphics.PreferredBackBufferHeight / 2);
            ballSpeed = 100f;

            base.Initialize();
        }

        protected override void LoadContent()
        {
            _spriteBatch = new SpriteBatch(GraphicsDevice);

            ballTexture = Content.Load<Texture2D>("ball");
        }

        protected override void Update(GameTime gameTime)
        {
            if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed ||
                                 Keyboard.GetState().IsKeyDown(Keys.Escape))
                Exit();

            // TODO: Add your update logic here

            // The time since Update was called last.
            float updatedBallSpeed = ballSpeed * (float)gameTime.ElapsedGameTime.TotalSeconds;

            var kstate = Keyboard.GetState();

            if (kstate.IsKeyDown(Keys.Up))
            {
                ballPosition.Y -= updatedBallSpeed;
            }

            if (kstate.IsKeyDown(Keys.Down))
            {
                ballPosition.Y += updatedBallSpeed;
            }

            if (kstate.IsKeyDown(Keys.Left))
            {
                ballPosition.X -= updatedBallSpeed;
            }

            if (kstate.IsKeyDown(Keys.Right))
            {
                ballPosition.X += updatedBallSpeed;
            }

            base.Update(gameTime);
        }

        protected override void Draw(GameTime gameTime)
        {
            GraphicsDevice.Clear(Microsoft.Xna.Framework.Color.CornflowerBlue);

            _spriteBatch.Begin();
            _spriteBatch.Draw(ballTexture, ballPosition, Microsoft.Xna.Framework.Color.White);
            _spriteBatch.End();


            base.Draw(gameTime);

        }
    }
}
